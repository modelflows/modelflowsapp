---
layout: post
title: "Urban flow data"
type: "Numerical / Urban Flow CFD"
tldr: "Urban canopy CFD data for building-array flow and passive scalar dispersion studies"
order: 3
---

### Data index:
   * [Urban LES and wind tunnel database — AIJ benchmark geometries](#aij-data)
   * [9 buildings canonical configuration - Equispaced Array](#urban-9block-equispaced)
   * [9 buildings canonical configuration - Variable Height and Distance Array](#urban-9block-variable)
   * [Urban wind tunnel database - EWTL Hamburg reference](#ewtl-data)
   * [Street canyon dispersion database — CODASC reference data](#codasc-exp)

## Urban LES and wind tunnel database — AIJ benchmark geometries<a id="aij-data"></a>
This entry brings together reference wind-tunnel measurements and three-dimensional large-eddy simulation data for urban configurations from the Architectural Institute of Japan (AIJ) benchmark collection. The experimental component corresponds to AIJ Case C, a 3 × 3 building-block array composed of eight surrounding cubic buildings of equal height H and a central building whose height varies across three sub-cases (flush/0H, equal/1H, or double/2H), tested at wind directions of 0°, 22.5°, and 45°, with point-wise mean velocity measurements taken at pedestrian height (z ≈ 0.02H). The numerical component provides time-resolved flow fields from OpenFOAM LES simulations using a WALE subgrid-scale model and a synthetic-turbulence inlet derived from the measured wind-tunnel profiles for four AIJ configurations: the Niigata city district, a real university campus including terrain elevation, and canonical arrays of 9 × 9 and 14 × 9 equispaced cubic buildings. These simulations were validated against the corresponding wind-tunnel measurements and provide time series of pressure and the three velocity components, offering both standard experimental reference data and full flow fields for validating urban canopy CFD simulations.

[[Link to AIJ data sets](https://www.aij.or.jp/jpn/publish/cfdguide/index_e.htm)]

## 9 buildings canonical configuration - Equispaced Array<a id="urban-9block-equispaced"></a>
This database contains data from three-dimensional CFD simulations of turbulent flow around a 3x3 array of 9 cubic buildings, each 0.2 m x 0.2 m x 0.2 m (H = 0.2 m), 
equispaced with a distance of 0.2 m between buildings, reproducing a layout similar to the AIJ Case C wind tunnel benchmark. Unlike the AIJ benchmark,
simulations were run varying the Reynolds number, the wind direction, and the emission rate of a passive scalar released into the flow. 
The dataset comprises 250 simulation cases, provided in .vtu (native solver mesh) and .npy (interpolated onto an equispaced grid) formats.

Database available *coming soon*.

## 9 buildings canonical configuration - Variable Height and Distance Array<a id="urban-9block-variable"></a>
This database contains data from three-dimensional CFD simulations of turbulent flow around a 3x3 array of 9 buildings of varying height, with H = 0.2 m 
and building heights of 1H, 2H, and 3H, and a variable distance between buildings, unlike the equispaced layout of the first dataset.
Simulations were run varying the Reynolds number, the wind direction, and the emission rate of a passive scalar.
The dataset comprises 243 simulation cases, provided in .vtu (native solver mesh) and .npy (interpolated onto an equispaced grid) formats.

Database available *coming soon*.


## Urban wind tunnel database — EWTL Hamburg reference data sets<a id="ewtl-data"></a>
This collection gathers the reference data sets of the Environmental Wind Tunnel Laboratory of the University of Hamburg, comprising boundary layer wind tunnel measurements of flow and pollutant dispersion over idealized and realistic urban and industrial layouts, including the CEDVAL and CEDVAL-LES compilations, the COST Action ES1006 cases (Michelstadt and CUTE) and the COST Action 732 cases (MUST and Oklahoma City), with variations of wind direction, source location and release type. Unlike CFD databases, the data are physical measurements taken point by point with laser Doppler anemometry and fast flame ionization detectors, so the spatial coverage differs from case to case: some data sets sample a three-dimensional arrangement of measurement positions, whereas others are restricted to two-dimensional planes or to vertical profiles at selected locations, generally denser close to the ground. In all cases the flow is characterized in a statistically stationary sense, through time-averaged statistics (mean values, variances and higher moments, and in some cases point time series at individual probes). The data are distributed as tabulated measurement files and are password protected, available on request from the laboratory.

[[Link to EWTL data sets](https://www.mi.uni-hamburg.de/en/arbeitsgruppen/windkanallabor/data-sets.html)]

## Street canyon dispersion database — CODASC reference data<a id="codasc-exp"></a>
The COncentration Data of Street Canyons (CODASC) database provides atmospheric boundary layer wind-tunnel measurements of traffic-like pollutant (SF6 tracer gas) concentrations in idealized street canyons, established by the Laboratory of Building- and Environmental Aerodynamics at the Karlsruhe Institute of Technology (KIT). The dataset covers 28 street-canyon/tree-avenue configurations spanning different canyon aspect ratios (W/H), wind directions, and avenue-tree arrangements (tree stand density, crown porosity), with wall-point concentration data on the leeward (Wall A) and windward (Wall B) sides as the primary output, plus supporting inflow velocity/TKE profiles for boundary-condition setup. It is a standard experimental reference for validating urban street-canyon dispersion models.

[[Link to CODASC experimental data](https://www.umweltaerodynamik.de/bilder-originale/CODA/CODASC.html)]
