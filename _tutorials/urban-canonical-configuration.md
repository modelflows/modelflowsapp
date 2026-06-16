---
layout: page
title: "Urban CFD with OpenFOAM: AIJ Case C"
category: "CFD & High-Fidelity Simulations"
tldr: "A practical guide to setting up RANS-based urban wind simulations using Blender, OpenFOAM and ParaView, demonstrated on the AIJ Case C benchmark."
author: "Your Name"
---

# Urban CFD with OpenFOAM: AIJ Case C

## Overview

Computational Fluid Dynamics (CFD) is widely used to predict wind conditions in urban environments — for example, to assess pedestrian comfort, natural ventilation, or pollutant dispersion around buildings. This tutorial teaches you how to run a complete urban wind simulation using open-source tools, from building geometry to results visualisation.

We use the **AIJ Case C** benchmark as a concrete example throughout. This is a standard test case with publicly available wind tunnel data, making it an ideal starting point for learning urban CFD.

**Tools used:**

| Tool | Purpose |
|------|---------|
| [Blender](https://www.blender.org/) | Building geometry and STL export |
| [OpenFOAM 12](https://openfoam.org/) | RANS CFD solver |
| [ParaView](https://www.paraview.org/) | Results visualisation |

---

## The AIJ Case C Benchmark

### Urban Wind and Pedestrian Comfort

As cities grow denser and taller, the wind environment at street level becomes increasingly important. Strong wind acceleration between buildings can create discomfort or even safety hazards for pedestrians, while poor ventilation in urban canyons traps pollutants and heat. Understanding and predicting these effects before buildings are constructed is a key challenge in modern urban planning.

CFD simulation has become an essential tool for this purpose. It can provide detailed, three-dimensional wind data across an entire neighbourhood at a fraction of the cost and time of physical wind tunnel testing, and can be integrated into the design process from early stages. However, before trusting CFD results for real design decisions, it is necessary to verify that the simulation setup is producing physically correct results. This is where benchmark validation comes in.

### The Architectural Institute of Japan (AIJ)

The **Architectural Institute of Japan (AIJ)** is a professional organisation for architects, engineers, and building designers, founded in 1886 with over 38,000 members. Among its contributions to the field, the AIJ has published a set of standard benchmark test cases specifically designed for validating CFD tools applied to pedestrian wind comfort around buildings. These benchmarks provide:

- Carefully controlled wind tunnel experimental data
- Clear geometry specifications
- Defined measurement point locations
- Guidelines for CFD setup and reporting

The AIJ benchmarks are now widely adopted internationally as the reference standard for urban wind CFD validation.

### AIJ Case C

Case C represents a **3×3 array of cubic buildings** with a variable-height building at the center, intended to model a simplified high-density urban block. Three configurations are defined by the height of the central building:

| Configuration | Central building height |
|--------------|------------------------|
| Case 0H | No central building |
| Case 1H | Same height as surrounding buildings |
| Case 2H | Twice the height of surrounding buildings |

![AIJ Case C](https://raw.githubusercontent.com/modelflows/modelflowsapp/software/Apps/Urban/assets/img/tutorial-aij/1.png)

Wind tunnel measurements of pedestrian-level wind speed are available for **9 scenarios**: 3 configurations × 3 wind directions (0°, 22.5°, 45°). Measurement points are located at z = 0.1D above the ground — the standard pedestrian reference height used in wind comfort assessments.

This case captures several flow features typical of real urban environments: wind acceleration through street canyons, recirculation in building wakes, and the strong influence of building height variation on pedestrian-level conditions.

---

## Step 1 — Geometry Generation with Blender

### What is Blender?

[Blender](https://www.blender.org/) is a free, open-source 3D modelling tool. For urban CFD, we use it to build simple building geometries and export them as **STL files**, which OpenFOAM reads to generate the mesh around the buildings.

You do not need to know Blender in depth — the operations needed for urban CFD are straightforward.

### Building the AIJ Case C geometry

The 3×3 array consists of identical cubic buildings (0.2 m × 0.2 m × 0.2 m) on a regular grid with a street width of 0.2 m between them.

**Steps:**

1. Open Blender. Delete the default cube: press `X` → **Delete**

2. Add the first building: `Shift+A → Mesh → Cube`

3. Press `N` to open the Item panel. Set dimensions to `0.2 m × 0.2 m × 0.2 m`

4. To generate the full 3×3 grid, use the **Array Modifier**:
   - In **Properties → Modifier**, click **Add Modifier → Array**
   - Set **Count = 3**, **Relative Offset X = 2.0**
   - Apply, then add a second Array modifier for Y with the same settings

5. Add the central building separately (`Shift+A → Mesh → Cube`) and set its height according to the configuration (Case 1H: 0.2 m, Case 2H: 0.4 m). Position it at the center of the grid.

<!-- IMAGE NEEDED: Blender viewport showing the completed 3×3 array (Case 2H) from an
     isometric view, with the taller central building visible -->

6. Select all: `A`

7. Export: **File → Export → Stl (.stl)**
   - Enable **Selection Only** and **Apply Modifiers**
   - Scale = 1.0
   - Save as `buildings.stl`

<!-- IMAGE NEEDED: Blender STL export dialog with the correct options highlighted -->

8. Place the exported file in your OpenFOAM case:
     constant/triSurface/buildings.stl
---

## Step 2 — OpenFOAM Simulation

### What is OpenFOAM?

[OpenFOAM](https://openfoam.org/) is a free, open-source CFD framework. It solves the fluid flow equations on an unstructured mesh using the Finite Volume Method. For urban wind simulation, we use the **steady-state RANS** (Reynolds-Averaged Navier-Stokes) solver, which is the standard approach in engineering practice.

In OpenFOAM 12, the solver is launched with:

```bash
foamRun
```

and the solver type is specified in `system/controlDict` as `incompressibleFluid`.

### Case directory structure

An OpenFOAM case is a folder with three subdirectories:
```
case/
├── 0/          ← initial and boundary conditions
├── constant/   ← mesh, geometry, physical properties
└── system/     ← solver settings, numerical schemes
```
---

### The `0/` directory — Boundary and Initial Conditions

Each file in `0/` defines one flow variable. For urban wind simulation you need:

| File | Variable | Description |
|------|---------|-------------|
| `U` | Velocity | Wind speed vector field |
| `p` | Pressure | Kinematic pressure |
| `k` | Turbulent kinetic energy | Intensity of turbulent fluctuations |
| `epsilon` | Turbulent dissipation rate | Rate at which turbulence energy is destroyed |
| `nut` | Turbulent viscosity | Effective viscosity due to turbulence |

Each file specifies what happens at every boundary patch. The table below summarises the boundary condition choices:

| Patch | U | p | k | epsilon | nut |
|-------|---|---|---|---------|-----|
| `inlet` | `atmBoundaryLayerInletVelocity` | `zeroGradient` | `atmBoundaryLayerInletK` | `atmBoundaryLayerInletEpsilon` | `calculated` |
| `outlet` | `inletOutlet` | `fixedValue 0` | `zeroGradient` | `zeroGradient` | `calculated` |
| `bottom` | `fixedValue (0 0 0)` | `zeroGradient` | `kqRWallFunction` | `epsilonWallFunction` | `nutkAtmRoughWallFunction` |
| `top` | `slip` | `zeroGradient` | `zeroGradient` | `zeroGradient` | `calculated` |
| `buildings` | `fixedValue (0 0 0)` | `zeroGradient` | `kqRWallFunction` | `epsilonWallFunction` | `nutUSpaldingWallFunction` |

**Why these choices?**

- **Inlet — ABL profile family:** Real urban wind follows a logarithmic profile where speed increases with height and turbulence decreases. The `atmBoundaryLayer*` family applies this profile consistently across U, k, and epsilon.
- **Outlet — `inletOutlet`:** Handles backflow gracefully by switching to an inlet condition wherever flow re-enters the domain.
- **Ground — wall functions with roughness:** Rather than resolving the very thin viscous sublayer, wall functions model its effect. `nutkAtmRoughWallFunction` accounts for terrain roughness.
- **Buildings — `nutUSpaldingWallFunction`:** More accurate than standard log-law wall functions for smooth surfaces, and works across a range of y+ values.
- **Top — `slip`:** The top of the domain is far from the buildings. A slip condition avoids artificially blocking the flow.

**Initial conditions**

The initial conditions set the starting values inside the domain before the solver begins iterating:

```cpp
// 0/U
internalField   uniform (0 3.0 0);   // wind blowing in Y direction

// 0/p
internalField   uniform 0;

// 0/k
internalField   uniform 0.22;

// 0/epsilon
internalField   uniform 2.05;

// 0/nut
internalField   uniform 1e-5;
```

> k and epsilon are estimated from the ABL inlet profile at a representative height. Starting close to the expected solution reduces the number of iterations needed to converge.

---

### The `constant/` directory

| File | Purpose |
|------|---------|
| `triSurface/buildings.stl` | Building geometry for snappyHexMesh |
| `physicalProperties` | Kinematic viscosity of air |
| `momentumTransport` | Turbulence model selection |

**`constant/momentumTransport`**

```cpp
simulationType  RAS;

RAS
{
    model           kEpsilon;
    turbulence      on;
    printCoeffs     on;
}
```

We use the standard **k-ε model**, which is the reference turbulence model for the AIJ benchmarks and the most widely used in urban wind engineering.

---

### The `system/` directory

| File | Purpose |
|------|---------|
| `controlDict` | Solver type, run time, write frequency |
| `blockMeshDict` | Background mesh definition |
| `snappyHexMeshDict` | Mesh refinement around buildings |
| `fvSchemes` | Numerical discretisation schemes |
| `fvSolution` | Solver tolerances and relaxation factors |
| `topoSetDict` | Identifies inlet/outlet faces on the cylindrical surface |
| `createPatchDict` | Creates inlet/outlet patches |

---

### Best Practice 1 — Cylindrical Domain

For urban CFD, a **cylindrical computational domain** is strongly preferred over a rectangular box.

<!-- IMAGE NEEDED: side-by-side diagram comparing rectangular vs cylindrical domain,
     both with wind direction arrows. Show how rectangular requires a different
     mesh orientation for each wind angle, while cylindrical uses the same mesh -->

**Why cylindrical?**

With a rectangular domain, the inlet and outlet must be on specific faces, which means a different mesh is needed for every wind direction. With a cylindrical domain, the entire lateral surface is a single patch that can be dynamically split into inlet and outlet based on wind direction — the same mesh works for all angles.

**Domain dimensions:**

| Parameter | Value |
|-----------|-------|
| Diameter | 40H |
| Height | 6H |
| Blockage ratio (area) | < 3% |
| Blockage ratio (height/width) | < 17% |

Keeping the blockage ratio below these thresholds ensures the domain boundaries do not artificially accelerate the flow around the buildings.

**Automatic inlet/outlet assignment with `topoSet` and `createPatch`**

For a given wind direction angle θ, the lateral surface is split using `topoSet` with `rotatedBoxToFace`, followed by `createPatch`. A rotated box selects all faces on the upwind half of the cylinder — these become `inlet`; the rest become `outlet`.

A Python script computes the box orientation vectors from θ:

```python
import math

def daps_vectors(theta_deg):
    """
    Compute i, j vectors for inlet/outlet splitting.
    theta: meteorological wind angle (degrees, clockwise from North)
    """
    theta = math.radians(theta_deg)
    ix =  math.sin(theta)
    iy =  math.cos(theta)
    # j perpendicular to i, ensuring i×j points upward (+z)
    jx = -iy
    jy =  ix
    return ix, iy, jx, jy
```

In `system/topoSetDict`:

```cpp
actions
(
    {
        name    inletFaces;
        type    faceSet;
        action  new;
        source  rotatedBoxToFace;
        sourceInfo
        {
            origin  (0 0 0);
            i       (ix iy 0);
            j       (jx jy 0);
            k       (0  0  6H);
            min     (-R -R 0);
            max     ( R  0 6H);
        }
    }
);
```

In `system/createPatchDict`:

```cpp
patches
(
    {
        name            inlet;
        patchInfo { type patch; }
        constructFrom   set;
        set             inletFaces;
    }
    {
        name            outlet;
        patchInfo { type patch; }
        constructFrom   set;
        set             outletFaces;
    }
);
```

---

### Best Practice 2 — Second-Order Discretisation

In `system/fvSchemes`, always use second-order schemes for convection terms:

```cpp
divSchemes
{
    default          none;
    div(phi,U)       Gauss linearUpwind grad(U);
    div(phi,k)       Gauss linearUpwind grad(k);
    div(phi,epsilon) Gauss linearUpwind grad(epsilon);
}
```

First-order schemes (e.g. `Gauss upwind`) introduce numerical diffusion — an artificial smearing of gradients that reduces accuracy. Second-order schemes are required by the AIJ guidelines for benchmark validation.

---

### Best Practice 3 — Strict Convergence Criteria

In `system/fvSolution`, set tight residual tolerances:

```cpp
SIMPLE
{
    residualControl
    {
        U       1e-5;
        p       1e-5;
        k       1e-5;
        epsilon 1e-5;
    }
}
```

Loose tolerances may stop the solver before the solution has truly stabilised, especially in recirculation zones behind buildings. In addition to residuals, monitor the velocity at a probe point in the wake — the solution is converged when this value stops changing between iterations.

---

### Best Practice 4 — Empty Domain Simulation

**Before running any simulation with buildings, always run an empty domain simulation first.**

<!-- IMAGE NEEDED: diagram of the empty cylindrical domain (no buildings) with the
     ABL inlet profile shown on one side, and two vertical monitoring lines marked:
     one at the inlet and one 15H downstream -->

**Why?** The ABL inlet profile can be distorted as it travels through the domain due to numerical diffusion and wall boundary conditions. If the profile changes significantly before reaching the buildings, the wind conditions acting on them are not what you intended.

**How to run it:** Remove the buildings STL, run `blockMesh` only (skip `snappyHexMesh`), then run `foamRun`.

**What to check:** Extract vertical profiles of U and k at the inlet and at 15H downstream. The profiles should agree within acceptable limits:

- U: deviation < 5%
- k: deviation < 10%

If deviations are too large, adjust the inlet roughness length z₀ or friction velocity u*.

<!-- IMAGE NEEDED: plot showing two overlaid vertical profiles of U/Uref vs z/H:
     solid line = inlet profile, dashed line = profile at 15H downstream.
     They should nearly overlap, demonstrating ABL self-preservation -->

---

### Best Practice 5 — Mesh Convergence Analysis

**Never trust results from a single mesh.** Always verify that refining the mesh does not significantly change the results.

**Why two sampling lines — windward and leeward?**

The windward profile is in the undisturbed approach flow, where mesh requirements are modest. The leeward profile is in the building wake, where the flow is more complex and mesh-sensitive. Checking both ensures the mesh is adequate in the most demanding region.

<!-- IMAGE NEEDED: top-view diagram of the cylindrical domain showing the building array
     at center, with two vertical sampling lines marked:
     Y = -0.8 m (windward, upstream) and Y = 1.0 m (leeward, downstream of central building) -->

**How to extract profiles with `sampleLines`**

Add to `system/controlDict`:

```cpp
functions
{
    sampleLines
    {
        type                sets;
        libs                ("libsampling.so");
        writeControl        writeTime;
        interpolationScheme cellPoint;
        setFormat           csv;
        fields              (U k epsilon);
        sets
        (
            windward
            {
                type    uniform;
                axis    z;
                start   (0 -0.8 0.001);
                end     (0 -0.8 1.2);
                nPoints 41;
            }
            leeward
            {
                type    uniform;
                axis    z;
                start   (0 1.0 0.001);
                end     (0 1.0 1.2);
                nPoints 41;
            }
        );
    }
}
```

**GCI method**

Run simulations on at least three mesh levels (Coarse, Medium, Fine). For each pair, compute the **Grid Convergence Index (GCI)**:

$$GCI = F_s \frac{|e|}{r^p - 1}$$

where e is the relative error between meshes, r is the refinement ratio, p is the observed order of convergence, and F_s = 1.25 is a safety factor. GCI values below 10% indicate the solution is mesh-independent.

<!-- IMAGE NEEDED: bar chart or table graphic showing GCI values for the three mesh pairs
     (Coarse/Medium, Medium/Fine, Coarse/Fine) for both windward and leeward lines,
     all bars below the 10% threshold line -->

---

### Running the simulation

**Sequential:**

```bash
blockMesh
surfaceFeatures
snappyHexMesh -overwrite
topoSet
createPatch -overwrite
foamRun
```

**Parallel:**

```bash
blockMesh
surfaceFeatures
snappyHexMesh -overwrite
topoSet
createPatch -overwrite
decomposePar
mpirun -np 8 foamRun -parallel
reconstructPar
```

Replace `8` with the number of available CPU cores, and set `numberOfSubdomains 8` in `system/decomposeParDict`.

**Convert results for ParaView:**

```bash
foamToVTK
```

<!-- IMAGE NEEDED: residual convergence plot showing U, k, epsilon on a log scale
     vs iteration number, all reaching the 1e-5 target -->

---

## Step 3 — Post-processing with ParaView

[ParaView](https://www.paraview.org/) is a free, open-source visualisation tool for simulation data.

### Opening the results

1. Open ParaView
2. **File → Open** → navigate to `case/VTK/` → select the `.vtk` file
3. Click **Apply**

### Velocity contour map at pedestrian height

1. **Filters → Common → Slice**
2. Normal: `(0, 0, 1)`, Origin: `(0, 0, 0.02)`
3. **Apply**
4. Set colour variable to `U` magnitude and click **Rescale**

<!-- IMAGE NEEDED: ParaView velocity magnitude contour map at z = 0.02 m, top view,
     0° wind direction. Annotate: acceleration corridors between buildings,
     recirculation zone behind the central building -->

### Extracting velocity profiles

1. **Filters → Data Analysis → Plot Over Line**
2. Point 1: `(0, -0.8, 0)` → Point 2: `(0, -0.8, 1.2)` for the windward line
3. **Apply**, then **File → Save Data** to export as CSV

Repeat for the leeward line `(0, 1.0, 0)` → `(0, 1.0, 1.2)`.

### Streamlines

1. **Filters → Common → Stream Tracer**
2. Seed type: **Line**, placed across the inlet
3. **Apply**, colour by `U` magnitude

<!-- IMAGE NEEDED: ParaView streamline visualisation coloured by velocity magnitude,
     showing flow deflection over and around the building array (3D perspective view) -->

---
