---
layout: page
title: "OpenFOAM RANS simulation of the DLR CH4/H2/N2 turbulent diffusion flame"
permalink: /software/tutorials/2026-combustion-tutorial/
---

# OpenFOAM RANS Simulation of the DLR CH4/H2/N2 Turbulent Diffusion Flame

## Overview

This tutorial describes a workflow for simulating the DLR CH4/H2/N2 turbulent diffusion flame using OpenFOAM-v10 and the `reactingFoam` solver.

The tutorial is designed for combustion dataset generation. It explains how to prepare the computational domain, define the boundary conditions, configure the physical and numerical models, run the simulation, validate the temperature field, and organize the CFD outputs for reduced-order modelling.

The workflow can be used as a starting point for:

- RANS simulation of turbulent non-premixed flames;
- OpenFOAM combustion case setup;
- CFD validation using experimental temperature profiles;
- parametric dataset generation;
- reduced-order modelling and data-driven surrogate modelling.

## Workflow

Geometry and mesh generation → Boundary conditions → OpenFOAM `reactingFoam` simulation → Post-processing and validation → CFD dataset assembly 

## Physical configuration

The reference case is the DLR turbulent non-premixed jet flame. The burner consists of a central fuel jet and a surrounding coaxial air stream. The schematic of the physical configuration is shown below.

<!-- IMAGES -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/DLR_burner_Geometry.png?raw=true" alt="DLR burner geometry" width="60%">
</p>

| Quantity | Description |
|---|---|
| Fuel stream | CH4/H2/N2 mixture |
| Fuel nozzle diameter | 8 mm |
| Coflow stream | Dry air |
| Coflow nozzle diameter | 140 mm |
| Computational domain | Axisymmetric wedge with external ambient region |
| Main objective | Generate validated CFD fields for reduced-order modelling |

The fuel composition is given in volumetric fractions as

$$X_{\mathrm{CH_4}} = 0.221,\qquad X_{\mathrm{H_2}} = 0.332,\qquad X_{\mathrm{N_2}} = 0.447.$$

OpenFOAM species fields are prescribed as mass fractions. After conversion, the fuel-inlet mass fractions are

$$Y_{\mathrm{CH_4}} = 0.2118,\qquad Y_{\mathrm{H_2}} = 0.0400,\qquad Y_{\mathrm{N_2}} = 0.7482.$$

The coflow and ambient streams are treated as dry air:

$$Y_{\mathrm{O_2}} = 0.233,\qquad Y_{\mathrm{N_2}} = 0.767.$$

The fuel and air streams are initialized at 292 K and atmospheric pressure.

## The structure of this case

The OpenFOAM case is organized using the standard case structure:

```text
DLR-LTS_Valid/
├── 0/
│   ├── alphat
│   ├── CH4
│   ├── epsilon
│   ├── G
│   ├── H2
│   ├── H2O
│   ├── k
│   ├── N2
│   ├── nut
│   ├── O2
│   ├── omega
│   ├── p
│   ├── T.orig
│   ├── U
│   └── Ydefault
│
├── chemkin/
│   ├── KEE58.dat
│   ├── thermo30.dat
│   └── transportProperties
│
├── constant/
│   ├── polyMesh/
│   ├── chemistryProperties
│   ├── combustionProperties
│   ├── g
│   ├── momentumTransport
│   ├── physicalProperties
│   ├── reactionsKEE
│   └── thermo.compressibleGas
│
└── system/
    ├── blockMeshDict
    ├── controlDict
    ├── decomposeParDict
    ├── fvSchemes
    ├── fvSolution
    ├── sample
    └── setFieldsDict
```

The `0/` folder contains the initial and boundary conditions for velocity, pressure, temperature, turbulence variables, radiation-related fields, and chemical species. The `chemkin/` folder contains the chemical kinetic and thermodynamic files. The `constant/` folder defines the thermophysical properties, turbulence model, combustion model, chemistry settings, gravity, and mesh. The `system/` folder contains the mesh-generation file, numerical schemes, solver settings, sampling settings, field initialization settings, and parallel-decomposition settings.

## Step 1. Geometry generation and mesh

The computational domain is represented as an axisymmetric wedge. This reduces computational cost while keeping the main flame structure. The domain includes:

- central fuel inlet;
- coaxial air inlet;
- external ambient-air inlet;
- burner wall and burner tip;
- lateral open boundary;
- downstream outlet;
- wedge planes;
- symmetry axis.

The geometry is generated using `blockMesh`. The main idea is to divide the radial direction into three physical regions:

1. **Fuel region:** central CH4/H2/N2 jet.
2. **Coflow air region:** coaxial dry-air stream.
3. **External ambient region:** surrounding air region used to allow entrainment.

The axial direction includes a short upstream/reverse section and a long downstream flame-development section. The mesh is refined near the fuel jet, burner tip, and shear-layer region, where the largest gradients in velocity, temperature, and species are expected.

The `blockMeshDict` script is as follows:

```cpp
/*--------------------------------*- C++ -*----------------------------------*\
  =========                 |
  \\      /  F ield         | OpenFOAM: The Open Source CFD Toolbox
   \\    /   O peration     | Website:  https://openfoam.org
    \\  /    A nd           | Version:  10
     \\/     M anipulation  |
\*---------------------------------------------------------------------------*/
FoamFile
{
    format      ascii;
    class       dictionary;
    object      blockMeshDict;
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * //

convertToMeters 0.001;

R1X 3.99619288633;
R2X 4.49571699712;
R3X 69.93337551073;
R4X 189.81916210055;

R1Y 0.17447754946;
R2Y 0.19628724314;
R3Y 3.05335711557;
R4Y 8.28768359941;

R1Ym -0.17447754946;
R2Ym -0.19628724314;
R3Ym -3.05335711557;
R4Ym -8.28768359941;

L  1000;
Lm -20;

vertices
(
    (0       0        0)    
    ($R1X    $R1Y     0)    
    ($R1X    $R1Y     $L)   

    (0       0        $L)   
    ($R1X    $R1Ym    0)    
    ($R1X    $R1Ym    $L)   

    (0       0        $Lm)  
    ($R1X    $R1Y     $Lm)  
    ($R1X    $R1Ym    $Lm)  

    ($R2X    $R2Y     0)    
    ($R2X    $R2Ym    0)    
    ($R2X    $R2Y     $L)  
    ($R2X    $R2Ym    $L)   

    ($R3X    $R3Y     0)    
    ($R3X    $R3Ym    0)    
    ($R3X    $R3Y     $L)   
    ($R3X    $R3Ym    $L)   

    ($R2X    $R2Y     $Lm)  
    ($R3X    $R3Y     $Lm)  
    ($R3X    $R3Ym    $Lm)  
    ($R2X    $R2Ym    $Lm)  

    ($R4X    $R4Y     0)    
    ($R4X    $R4Ym    0)    
    ($R4X    $R4Y     $L)   
    ($R4X    $R4Ym    $L)   
);

nFuel          7;
nBurner        1;
nCoflow        40;
nExternal      30;
nLength        200;
nLengthReverse 10;

gradingFuel          1;
gradingCoflow        6;
gradingLength        10;
gradingLengthInverse 0.5;

blocks
(
    // Fuel
    hex (6 8 7 6 0 4 1 0) ($nFuel 1 $nLengthReverse)
    simpleGrading ($gradingFuel  1 $gradingLengthInverse )

    hex (0 4 1 0 3 5 2 3) ($nFuel  1 $nLength)
    simpleGrading ($gradingFuel 1 $gradingLength)

    // Wall
    hex (4 10 9 1 5 12 11 2) ($nBurner 1 $nLength)
    simpleGrading (1 1 $gradingLength)

    // Coflow
    hex (20 19 18 17 10 14 13 9) ($nCoflow 1 $nLengthReverse)
    simpleGrading ($gradingCoflow  1 $gradingLengthInverse)
    hex (10 14 13 9 12 16 15 11) ($nCoflow 1 $nLength)
    simpleGrading ($gradingCoflow  1 $gradingLength)

    // External wall
    hex (14 22 21 13 16 24 23 15) ($nExternal 1 $nLength)
    simpleGrading (1  1 $gradingLength)
);

boundary
(
    inletfuel
    {
        type patch;
        faces
        (
            (6 8 7 6)
        );
    }

    inletair
    {
        type patch;
        faces
        (
            (19 20 17 18)
        );
    }

    outlet
    {
        type patch;
        faces
        (
            (5 3 3 2)
            (12 11 2 5)
            (16 15 11 12)
            (15 16 24 23)
        );
    }

    axis
    {
        type empty;
        faces
        (
            (3 0 0 3)
            (0 6 6 0)
        );
    }

    leftside
    {
        type patch;
        faces
        (
            (23 24 22 21)
            
        );
    }
    
    inletambient
    {
        type patch;
        faces
        (
            (14 13 21 22)
        );
    }

    burnerwall
    {
        type wall;
        faces
        (
            (8 7 1 4)
            (10 9 17 20)
            
            (19 18 13 14)
        );
    }

    burnertip
    {
        type wall;
        faces
        (
            (4 1 9 10)
        );
    }

    front
    {
        type wedge;
        faces
        (
            (1 0 3 2)
            (7 6 0 1)
            (9 1 2 11)
            (13 9 11 15)
            (18 17 9 13)
            (15 23 21 13)
        );
    }

    back
    {
        type wedge;
        faces
        (
            (5 3 0 4)
            (4 0 6 8)
            (12 5 4 10)
            (16 12 10 14)
            (19 14 10 20)
            (16 14 22 24)
        );
    }
);

// ************************************************************************* //
```

### Explanation of the mesh parameters

The length unit is converted from millimetres to metres using:

```cpp
convertToMeters 0.001;
```

The variables `R1X`, `R2X`, `R3X`, and `R4X` define the radial extents of the fuel, burner wall, coflow, and external ambient region. The corresponding `R1Y`, `R2Y`, `R3Y`, and `R4Y` values define the small wedge angle used for the axisymmetric calculation. The negative values `R1Ym`, `R2Ym`, `R3Ym`, and `R4Ym` define the opposite wedge plane.

The downstream computational length is controlled by `L = 1000`, corresponding to 1000 mm. A short upstream section is defined by `Lm = -20`, corresponding to 20 mm before the nominal burner exit.

The mesh resolution is controlled by:

```cpp
nFuel          7;
nBurner        1;
nCoflow        40;
nExternal      30;
nLength        200;
nLengthReverse 10;
```

Here, `nFuel`, `nCoflow`, and `nExternal` control the radial resolution in the fuel, coflow, and ambient regions. `nLength` controls the axial resolution in the downstream flame-development region, while `nLengthReverse` controls the short upstream/reverse section.

The mesh stretching is controlled by:

```cpp
gradingFuel          1;
gradingCoflow        6;
gradingLength        10;
gradingLengthInverse 0.5;
```

The mesh contains five main hexahedral blocks: the fuel reverse section, fuel downstream section, burner-wall section, coflow section, and external ambient section. The main boundary patches are `inletfuel`, `inletair`, `inletambient`, `outlet`, `leftside`, `burnerwall`, `burnertip`, `front`, `back`, and `axis`.

The mesh is generated using:

```bash
blockMesh
checkMesh
```

Recommended checks after mesh generation include: no negative cell volumes; acceptable non-orthogonality and skewness.


## Step 2. Boundary conditions

The main OpenFOAM fields used in the initial-condition folder are summarized below.

| Variable | Description | Unit |
|---|---|---|
| `U` | Velocity vector | m/s |
| `p` | Pressure | Pa |
| `T` or `T.orig` | Temperature | K |
| `CH4` | Methane mass fraction | - |
| `H2` | Hydrogen mass fraction | - |
| `H2O` | Water-vapor mass fraction | - |
| `O2` | Oxygen mass fraction | - |
| `N2` | Nitrogen mass fraction | - |
| `Ydefault` | Default species mass fraction used by the chemistry/thermophysical model | - |
| `k` | Turbulent kinetic energy | m²/s² |
| `epsilon` | Turbulent dissipation rate | m²/s³ |
| `nut` | Turbulent kinematic viscosity | m²/s |
| `alphat` | Turbulent thermal diffusivity | kg/(m·s) |
| `G` | Incident radiation field used by the radiation model | kg/s³ |

The boundary-condition strategy is summarized in the following table.

| Patch | Physical meaning | Main treatment |
|---|---|---|
| `inletfuel` | Central CH4/H2/N2 fuel jet | Mass-flow-rate velocity inlet; fixed fuel composition; fixed temperature; specified inlet turbulence |
| `inletair` | Coflow dry air | Fixed axial velocity; fixed dry-air composition; fixed temperature; specified inlet turbulence |
| `inletambient` | External ambient-air region | Open velocity boundary; ambient-air composition and temperature for inflow |
| `outlet` | Downstream outlet | Pressure-based outlet; `inletOutlet` treatment for scalar backflow |
| `leftside` | Outer lateral boundary | Open boundary allowing entrainment and outflow |
| `burnerwall` and `burnertip` | Burner wall and burner lip | No-slip velocity; zero-gradient temperature/species; wall functions for turbulence |
| `axis` | Symmetry axis | `empty` boundary for the axisymmetric wedge formulation |
| `front/back` | Wedge planes | `wedge` boundary condition |

### Fuel and air inlets

The fuel inlet is prescribed using a mass-flow-rate boundary condition:

```cpp
inletfuel
{
    type            flowRateInletVelocity;
    massFlowRate    constant 2.057718e-05;
    rhoInlet        0.698451;
    profile         turbulentBL;
}
```

The option `profile turbulentBL` imposes a turbulent-boundary-layer-type velocity profile at the fuel inlet. This is more representative of a turbulent pipe-flow exit than a uniform plug-flow profile.

The coflow air inlet is imposed as a fixed axial velocity:

```cpp
inletair
{
    type            fixedValue;
    value           uniform (0 0 0.3);
}
```

The pressure field is initialized at atmospheric pressure, while the temperature field is initialized at 292 K:

```cpp
p:  internalField   uniform 101325;
T:  internalField   uniform 292;
```

The fuel, coflow air, and ambient-air inlets are prescribed at 292 K.

### Species composition

The fuel inlet composition is prescribed using fixed mass fractions:

```text
CH4 = 0.2118
H2  = 0.0400
N2  = 0.7482
O2  = 0
H2O = 0
```

The coflow and ambient regions are treated as dry air:

```text
O2  = 0.233
N2  = 0.767
CH4 = 0
H2  = 0
H2O = 0
```

For open boundaries such as `outlet` and `leftside`, the scalar fields use `inletOutlet`-type conditions. This allows zero-gradient behavior for outflow and imposes ambient values only when backflow occurs. Solid walls use zero-gradient species boundary conditions.

### Turbulence and radiation fields

The turbulent kinetic energy is estimated from the turbulence intensity `I`:

$$k = \frac{3}{2}(I U)^2.$$

The dissipation rate is estimated using a mixing length `l`, which is typically defined as `l = 0.07 Lc`, where `Lc` is the characteristic length of the corresponding inlet region.

For example, the fuel inlet uses a turbulence intensity of 5%:

```cpp
inletfuel
{
    type            turbulentIntensityKineticEnergyInlet;
    intensity       0.05;
    value           uniform 6.7;
}
```

The burner wall and burner tip use standard wall functions for `k`, `epsilon`, `nut`, and `alphat`. The field `G` is the incident radiation field used by the radiation model. It is initialized as zero and uses a `MarshakRadiation` boundary condition on most patches. The front and back patches remain wedge boundaries.

## Step 3. OpenFOAM simulation

The simulation is performed with OpenFOAM-v10 using `reactingFoam`. The solver is selected in `system/controlDict`:

```text
application     reactingFoam;
```

This section summarizes the main files in `constant/` and `system/`. These files define the physics, chemistry, numerical schemes, solution algorithms, post-processing, and parallel execution.

### 3.1 Thermophysical model: `constant/physicalProperties`

The gas mixture is modeled as a reacting multi-component perfect gas. The thermophysical model is defined as:

```cpp
thermoType
{
    type            hePsiThermo;
    mixture         multiComponentMixture;
    transport       sutherland;
    thermo          janaf;
    energy          sensibleEnthalpy;
    equationOfState perfectGas;
    specie          specie;
}

defaultSpecie N2;

#include "thermo.compressibleGas"
```

The main choices are:

- `hePsiThermo`: compressible thermodynamics based on sensible enthalpy;
- `multiComponentMixture`: each chemical species is solved as an individual mass-fraction field;
- `perfectGas`: ideal-gas equation of state for the gas mixture;
- `janaf`: JANAF polynomial thermodynamic data;
- `sutherland`: Sutherland-law molecular transport;
- `sensibleEnthalpy`: energy equation written in terms of sensible enthalpy;
- `defaultSpecie N2`: nitrogen is used as the default species when required by the mixture model.

The species thermodynamic data are included from `thermo.compressibleGas`, which provides the thermodynamic and transport data.

### 3.2 Turbulence model: `constant/momentumTransport`

The case uses a RANS formulation with the standard `kEpsilon` turbulence model:

```cpp
simulationType   RAS;

RAS
{
    model           kEpsilon;

    kEpsilonCoeffs
    {
        C1 1.6;
    }

    turbulence      on;
    printCoeffs     on;
}
```

The turbulent viscosity is computed from the turbulent kinetic energy and dissipation rate:

$$\mu_t=\rho C_\mu\frac{k^2}{\varepsilon}.$$

In this tutorial case, the model coefficient `C1` is set to 1.6 instead of the default value 1.44. This empirical adjustment is used to improve the predicted jet spreading and flame development for the present RANS calculation.

### 3.3 Combustion model: `constant/combustionProperties`

Turbulence-chemistry interaction is modeled using the Eddy Dissipation Concept (EDC):

```cpp
combustionModel  EDC;

EDCCoeffs
{
    version     v2005;
}
```

The EDC model assumes that chemical reactions occur in fine turbulent structures. This makes it suitable for turbulent non-premixed combustion, where finite-rate chemistry and turbulent mixing both influence the flame. 

### 3.4 Chemistry and TDAC: `constant/chemistryProperties`

The chemical kinetics are activated and solved using an ODE-based chemistry solver:

```cpp
#includeEtc "caseDicts/solvers/chemistry/TDAC/chemistryPropertiesFlame.cfg"

chemistryType
{
    solver            ode;
}

chemistry       on;

initialChemicalTimeStep 1e-7;
```

The stiff chemical source terms are integrated using the `seulex` ODE solver:

```cpp
odeCoeffs
{
    solver          seulex;
    absTol          1e-8;
    relTol          1e-1;
}
```

TDAC acceleration is used to reduce the cost of detailed chemistry. The initial species set for reduction contains the two fuel components:

```cpp
reduction
{
    initialSet
    (
        CH4
        H2
    );
}
```

The temperature scale factor used for tabulation accuracy is defined as:

```cpp
tabulation
{
    scaleFactor
    {
        Temperature  1000;
    }
}
```

The reaction mechanism is included through:

```cpp
#include "reactionsKEE"
```

This mechanism file defines the chemical species and elementary reactions used by the reacting-flow simulation.

### 3.5 Gravity field: `constant/g`

The gravity vector is defined as:

```cpp
dimensions      [0 1 -2 0 0 0 0];
value           (0 0 -9.81);
```

Although gravity is not the dominant mechanism in this jet flame, it is defined consistently in the case because the selected solver and thermophysical setup can access the gravity field.

### 3.6 Time control and field averaging: `system/controlDict`

The reference case uses `reactingFoam`, starts from the latest available time, and runs to a pseudo-time value of 20000:

```cpp
application     reactingFoam;

startFrom       latestTime;
endTime         20000;
deltaT          1;

writeControl    runTime;
writeInterval   1000;
writeFormat     binary;
```

The case uses `fieldAverage` to compute time-averaged velocity and temperature fields after the solution has developed:

```cpp
functions
{
    fieldAverage1
    {
        type            fieldAverage;
        libs            ("libfieldFunctionObjects.so");

        fields
        (
            U
            {
                mean        on;
                prime2Mean  on;
                base        time;
            }
            T
            {
                mean        on;
                prime2Mean  off;
                base        time;
            }
        );

        timeStart       10000;
        timeEnd         20000;
    }
}
```

For this RANS tutorial, the local Euler pseudo-time is mainly used as an iteration-like convergence coordinate. The averaged fields are used for post-processing and validation after the initial transient iterations are excluded.

### 3.7 Numerical schemes: `system/fvSchemes`

The case uses a local Euler time scheme:

```cpp
ddtSchemes
{
    default         localEuler;
}
```

This choice is useful for accelerating convergence toward a steady RANS solution. Spatial gradients use Gauss linear discretization:

```cpp
gradSchemes
{
    default         Gauss linear;
}
```

The main convection schemes are bounded limited-linear schemes:

```cpp
divSchemes
{
    div(phi,U)          Gauss limitedLinearV 1;
    div(phi,Yi)         Gauss limitedLinear01 1;
    div(phi,h)          Gauss limitedLinear 1;
    div(phi,k)          Gauss limitedLinear 1;
    div(phi,epsilon)    Gauss limitedLinear 1;
}
```

### 3.8 Linear solvers and PIMPLE controls: `system/fvSolution`

The pressure equation is solved using a PCG solver with DIC preconditioning:

```cpp
p
{
    solver           PCG;
    preconditioner   DIC;
    tolerance        1e-6;
    relTol           0.01;
}
```

Velocity, enthalpy, and turbulence equations are solved using PBiCGStab with DILU preconditioning:

```cpp
"(U|h|k|epsilon|omega)"
{
    solver          PBiCGStab;
    preconditioner  DILU;
    tolerance       1e-6;
    relTol          0.1;
}
```

Species equations are solved with a tighter absolute tolerance:

```cpp
"Yi.*"
{
    solver          PBiCG;
    preconditioner  DILU;
    tolerance       1e-8;
    relTol          0.1;
}
```

The pressure-velocity coupling is handled by the PIMPLE algorithm:

```cpp
PIMPLE
{
    momentumPredictor   yes;
    nOuterCorrectors    1;
    nCorrectors         3;
    nNonOrthogonalCorrectors 0;

    maxDeltaT           1e-4;
    maxCo               0.25;
    alphaTemp           0.05;
    alphaY              0.05;
}
```

The small `maxCo` and damping coefficients help improve robustness for reacting-flow calculations with strong temperature and species gradients.

### 3.9 Parallel decomposition: `system/decomposeParDict`

For parallel calculations, the domain is decomposed using the `scotch` method:

```cpp
numberOfSubdomains 60;

method          scotch;
```

The number of subdomains should be adjusted according to the available CPU cores. For example, if 20 cores are used, `numberOfSubdomains` should be changed to 20 before running `decomposePar`.

### 3.10 Sampling and initialization: `system/sample` and `system/setFieldsDict`

The `sample` dictionary extracts radial temperature profiles at two axial locations:

```cpp
sets
(
    Z=40mm
    {
        type    lineFace;
        axis    x;
        start   (-0.001 0 0.04);
        end     (0.2 0 0.04);
        nPoints 1000;
    }
    Z=480mm
    {
        type    lineFace;
        axis    x;
        start   (-0.001 0 0.48);
        end     (0.2 0 0.48);
        nPoints 1000;
    }
);

fields          (T);
```

These two sampling lines are used to compare simulated radial temperature profiles with experimental data at `x = 40 mm` and `x = 480 mm`.

The `setFieldsDict` file can be used to initialize a high-temperature ignition region:

```cpp
defaultFieldValues
(
    volScalarFieldValue T 292
);

regions
(
    boxToCell
    {
        box (0.002 -0.01 0.005) (0.02 0.01 0.055);
        fieldValues
        (
            volScalarFieldValue T 2200
        );
    }
);
```

This initialization helps the reacting-flow calculation start from a physically ignited state.

## Step 4. Running the case

Run the case in serial:

```bash
blockMesh
checkMesh
reactingFoam
paraFoam
```

Run the case in parallel. The number of cores is set in `system/decomposeParDict`:

```bash
decomposePar
mpirun -np <number_of_processors> reactingFoam -parallel
reconstructPar
paraFoam
```

If an ignition region is required, initialize the temperature field before running the solver:

```bash
setFields
reactingFoam
```

During the simulation, monitor:

- residuals;
- mass-flow balance, etc.


## Step 5. Post-processing

Open the result in ParaView:

```bash
paraFoam
```

For validation, radial temperature profiles at `x = 40 mm` and `x = 480 mm` are compared with experimental data.

<!-- IMAGES -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/DLR_burner_Validation.png?raw=true" alt="DLR burner validation" width="70%">
</p>

The temperature profiles are extracted using the sampling lines defined in `system/sample`. The near-field profile at 40 mm is useful for evaluating flame anchoring and early mixing, while the downstream profile at 480 mm is useful for evaluating flame spreading, heat release distribution, and far-field mixing.


## Step 6. Data generation for Reduced-order modelling / AI

The converged CFD fields are organized into a structured dataset for reduced-order modelling. A representative parametric sweep contains:

| Parameter | Range |
|---|---|
| Reynolds number | 11000 to 20000 |
| Hydrogen mass fraction | 4% to 22% |
| Number of CFD cases | 100 |

For each case, the fuel velocity and mass flow rate are updated according to the target Reynolds number. The fuel composition is updated according to the target hydrogen mass fraction.

The retained variables for ROM/AI can include:

- velocity components;
- temperature;
- pressure;
- species mass fractions;
- turbulence quantities.

These data can be used for POD, DMD, tensor-based ROMs, interpolation models, and machine-learning surrogate models.
