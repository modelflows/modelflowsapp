---
layout: post
title: "Urban flow data"
type: "Numerical / Urban Flow CFD"
tldr: "Urban canopy CFD data for building-array flow and passive scalar dispersion studies"
order: 3
---

### Data index:
   * [9 buildings canonical configuration - Equispaced Array](#urban-9block-equispaced)
   * [9 buildings canonical configuration - Variable Height and Distance Array](#urban-9block-variable)
   * [AIJ - Benchmark geometris](#aij-data)
   * [Urban wind tunnel database - EWTL Hamburg reference](#ewtl-data)


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

## Urban LES database — AIJ benchmark geometries<a id="aij-data"></a>
This database contains data from three-dimensional large-eddy simulations of turbulent flow over four urban configurations taken from the AIJ wind tunnel benchmark collection: two real urban layouts (a city district and a university campus, the latter including terrain elevation) and two regular arrays of cubic buildings. Specifically, it provides time-varying flow fields for the Niigata city district and for a real university campus, together with the canonical wind tunnel configurations of 9 × 9 and 14 × 9 equispaced cubic buildings. Unlike the benchmark, which reports time-averaged measurements at sparse probe points, the simulations were run with OpenFOAM using a WALE subgrid-scale model and a synthetic-turbulence inlet built from the measured wind tunnel profiles, and were validated against those measurements, so that the full time-resolved flow fields are made available. Each case provides a time series of snapshots of pressure and the three velocity components, in .vtu (native solver mesh) and .npy (interpolated onto an equispaced grid, at a common spatial resolution and accompanied by a static building occupancy mask) formats.

[[Link to AIJ data sets](https://www.aij.or.jp/%20jpn/publish/cfdguide/index_e.htm)]

## Urban wind tunnel database — EWTL Hamburg reference data sets<a id="ewtl-data"></a>
This collection gathers the reference data sets of the Environmental Wind Tunnel Laboratory of the University of Hamburg, comprising boundary layer wind tunnel measurements of flow and pollutant dispersion over idealized and realistic urban and industrial layouts, including the CEDVAL and CEDVAL-LES compilations, the COST Action ES1006 cases (Michelstadt and CUTE) and the COST Action 732 cases (MUST and Oklahoma City), with variations of wind direction, source location and release type. Unlike CFD databases, the data are physical measurements taken point by point with laser Doppler anemometry and fast flame ionization detectors, so the spatial coverage differs from case to case: some data sets sample a three-dimensional arrangement of measurement positions, whereas others are restricted to two-dimensional planes or to vertical profiles at selected locations, generally denser close to the ground. In all cases the flow is characterized in a statistically stationary sense, through time-averaged statistics (mean values, variances and higher moments, and in some cases point time series at individual probes). The data are distributed as tabulated measurement files and are password protected, available on request from the laboratory.

[[Link to EWTL data sets](https://www.mi.uni-hamburg.de/en/arbeitsgruppen/windkanallabor/data-sets.html)]
