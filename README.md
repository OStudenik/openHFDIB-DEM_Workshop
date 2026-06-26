# OpenHFDIB-DEM Workshop

Workshop repository accompanying the **OpenHFDIB-DEM** short course prepared for the **21st OpenFOAM Workshop (Guimarães, 2026)**.

This repository contains:
- a local copy of the `openHFDIB-DEM` source tree used in the course,
- tutorial and demonstration cases organized by topic,
- auxiliary cases and templates used to build up more advanced examples.

The course is developed by the **Laboratory of Technical Mathematics (techMathGroup)** and provides a practical introduction to particle-resolved CFD-DEM simulations built on top of OpenFOAM.

## Course scope

The course introduces the main workflows needed to work with OpenHFDIB-DEM:
- general information about the library and its development philosophy,
- adding solid bodies to the computational domain,
- selecting and configuring body movement modes,
- setting up the Discrete Element Method (DEM),
- coupling CFD with DEM for resolved fluid-particle interaction simulations.

Potential future extensions include installation details, solver customization, advanced workflows, parallel execution, and post-processing.

## Related links

- OpenHFDIB-DEM repository: <https://github.com/techMathGroup/openHFDIB-DEM>
- Course playlist: <https://youtube.com/playlist?list=PLyB3_fxgRQeJlf7x8SO8BU94tpXlnaGrf&si=R-FZiiwmthm6y8qj>
- Workshop: 21st OpenFOAM Workshop, Guimarães, Portugal (2026)
- Laboratory webpage: <https://techmathgroup.isoz.eu>

## Repository layout

```text
openHFDIB-DEM_Workshop/
├── openHFDIB-DEM_com/      # library and solver sources used in the course
└── testCases/
    ├── 00_baseCase/        # minimal reference case
    ├── 01_solid_body_addition/
    ├── 02_solid_body_movement/
    ├── 03_DEM/
    ├── 04_CFD-DEM/
    └── otherCases/         # auxiliary and development/support examples
```

### `openHFDIB-DEM_com/`

This folder contains the OpenHFDIB-DEM code used during the workshop, including:
- `src/` for library sources,
- `applications/` for solver sources,
- `compileLib.sh` to compile the library,
- `compileSol.sh` to compile the solvers,
- `compileAll.sh` to compile both.

### `testCases/`

The tutorial cases are organized to follow the course progression.

#### `00_baseCase/`
A minimal starting point showing the basic case structure used throughout the workshop.

#### `01_solid_body_addition/`
Cases related to **Video 2: Adding solid bodies**.

Main examples:
- `01_single_body_addition/`
- `02_repeated_body_addition/`
- `03_glitters_and_impeller/`

These cases cover:
- adding a single solid body,
- repeated/random addition of bodies,
- defining spheres and STL-based geometries,
- working with convex and non-convex bodies,
- preparing geometry and mesh-related inputs.

#### `02_solid_body_movement/`
Cases related to **Video 3: Solid body movement modes**.

Main examples:
- `01_body_with_prescrtibed_rotation/`
- `02_freely_moving_body/`
- `03_glitters_and_impeller/`

These cases demonstrate:
- fixed and prescribed motion,
- rotational movement,
- freely moving bodies driven by forces and torques,
- runtime-generated body information such as positions, velocities, and orientations.

#### `03_DEM/`
Cases related to **Video 4: Discrete Element Method**.

Main examples:
- `01_particle_particle_collision/`
- `02_particle_wall_collision/`
- `03_glitters_and_impeller/`

These cases focus on:
- contact modeling,
- material and collision properties,
- DEM parameter selection,
- practical collision setups for simple and more applied examples.

#### `04_CFD-DEM/`
Cases related to **Video 5: Computational Fluid Dynamics - Discrete Element Method**.

Main example:
- `01_glitters_and_impeller/`

This folder combines the previous topics into a fully coupled CFD-DEM workflow.

#### `otherCases/`
Auxiliary material and support cases not central to the main tutorial path, including:
- helper or legacy setup workflows,
- intermediate body-creation examples,
- master/run case patterns,
- experimental or development-side case organization.

## How the tutorial cases work

Most tutorial folders follow the same structure:
- `0.org/` stores the template initial fields,
- `Allrun` recreates `0/` from `0.org/`, runs `blockMesh`, detects the solver from `system/controlDict`, and launches the simulation,
- `Allclean` removes generated files,
- `constant/HFDIBDEMDict` contains immersed-body and DEM-related configuration,
- `constant/triSurface/` contains STL geometries when applicable,
- `system/` contains the OpenFOAM case dictionaries.

A typical `Allrun` script in this repository:
1. deletes the generated `0/` directory,
2. copies `0.org/` to `0/`,
3. creates ParaView helpers,
4. runs `blockMesh`,
5. reads the application name from `system/controlDict`,
6. runs the configured solver.

## Prerequisites

To use this repository, you should already have:
- a working OpenFOAM installation,
- a shell environment with OpenFOAM sourced,
- a successful OpenHFDIB-DEM compilation,
- basic familiarity with OpenFOAM case structure and execution.

The case dictionaries in this repository use a structure consistent with modern OpenFOAM releases, and the included control files currently reference `HFDIBDEMFoam` as the main solver in the base case.

## Quick start

### 1. Compile the library and solvers

From the repository root:

```bash
cd openHFDIB-DEM_com
./compileAll.sh
```

You can also compile components separately:

```bash
cd openHFDIB-DEM_com
./compileLib.sh
./compileSol.sh
```

### 2. Run a tutorial case

Example:

```bash
cd testCases/01_solid_body_addition/01_single_body_addition
./Allrun
```

### 3. Open the results

Most cases prepare ParaView helper files automatically. You can open the case with:

```bash
paraFoam
```

or, depending on your setup:

```bash
paraFoam -builtin
```

## Suggested learning path

A practical order for working through the repository is:

1. `testCases/00_baseCase/`
2. `testCases/01_solid_body_addition/`
3. `testCases/02_solid_body_movement/`
4. `testCases/03_DEM/`
5. `testCases/04_CFD-DEM/`

This progression mirrors the course structure from geometry definition through fully coupled particle-resolved CFD-DEM simulations.

## Course video mapping

### Video 1 — General Introduction
General overview of:
- OpenHFDIB-DEM purpose,
- library architecture,
- key capabilities,
- application areas,
- documentation and learning resources.

This video is primarily conceptual and is complemented in this repository by the overall case organization and the included OpenHFDIB-DEM source tree in `openHFDIB-DEM_com/`.

### Video 2 — Adding solid bodies
Mapped mainly to:
- `testCases/01_solid_body_addition/`

### Video 3 — Solid body movement modes
Mapped mainly to:
- `testCases/02_solid_body_movement/`

This stage also introduces runtime body information outputs such as the `bodiesInfo` directory generated by applicable cases.

### Video 4 — Discrete Element Method
Mapped mainly to:
- `testCases/03_DEM/`

### Video 5 — CFD–DEM
Mapped mainly to:
- `testCases/04_CFD-DEM/`

### Video 6 — Installation of the library
Mapped mainly to:
- `openHFDIB-DEM_com/`

This includes the local source tree and the provided compile scripts used to build the workshop version of the library and its solvers.

## Notes

- The `otherCases/` folder is useful for advanced inspection, but most attendees should start with the numbered `00`–`04` tutorial folders.
- Generated runtime folders and files should generally be cleaned with `Allclean` before rerunning a case if you want a fresh start.

## Acknowledgement

The materials in this repository are based on the continuously developed open-source OpenHFDIB-DEM framework used in academic research and engineering applications involving fluid-particle interaction, particulate flows, and immersed boundary method.

If you find the course useful, consider starring the main OpenHFDIB-DEM repository and subscribing for future tutorials and updates.
