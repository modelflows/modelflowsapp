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
   * [Vallecas real-urban large-scale configuration, real terrain elevation and building array](#urban-vallecas)
   * [AIJ Case E - Niigata city district](#niigara-city-district)
   * [AIJ Case K - Regular 9×9 cubic array](#9x9-cubic-array)
   * [AIJ Case L - Regular 14×9 cubic array](#14x9-cubic-array)
   * [AIJ Case M - TPU university campus](#tpu-university-campus)

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

## Vallecas real-urban large-scale configuration, real terrain elevation and building array

This database contains data from three-dimensional CFD simulations of turbulent wind flow over the Vallecas district of Madrid, a real urban area with varying height and footprint set on real terrain elevation. The domain is a cylinder with a diameter of approximately 3 410 m and a vertical extent ranging between 317 m and 358 m. It is modelled with neutral atmospheric boundary layer conditions, computed with steady-state RANS and the $k$-$\varepsilon$ turbulence model (with simpleFoam). The ground is split into terrain, vegetation and water, each with its own surface roughness. Simulations were run varying the wind direction and reference wind speed at 5.5 m height. For each case the following fields are saved: U (mean velocity (m/s)), p (mean kinematic pressure (m²/s²)), k (turbulent kinetic energy (m²/s²)), epsilon (turbulent dissipation rate (m²/s³)), nut (turbulent eddy viscosity (m²/s)). In addition, traffic pollutants emitted from the nearby highways, with emission rates estimated from COPERT values, are transported as passive scalars, giving the concentration fields CO, NOx and PM (kg/m³). The dataset comprises 24 simulation cases, provided in .vtu format.

Database available *coming soon*.

## Urban LES database — AIJ Case E (Niigata city district)<a id="niigara-city-district"></a>
This database contains data from a three-dimensional large-eddy simulation of turbulent flow over a real urban district in Niigata (Japan), reproducing the geometry of the AIJ Case E wind tunnel benchmark at full scale (footprint of about 395 m × 395 m, tallest building H = 60 m). Unlike the benchmark, which reports time-averaged measurements at sparse probe points, the simulation was run with OpenFOAM (WALE subgrid-scale model, synthetic-turbulence inlet from the measured profile) and validated against those points, providing the full time-resolved fields. The dataset comprises 497 snapshots of pressure and the three velocity components, provided in .vtu (native solver mesh) and .npy (equispaced grid of 198 × 198 × 21 points at Δxy = 2 m, Δz = 5 m, with building mask) formats.

[[Link to EchoNet-Dynamic](https://www.aij.or.jp/%20jpn/publish/cfdguide/index_e.htm)]

## Urban LES database — AIJ Case K (regular 9×9 cubic array)<a id="9x9-cubic-array"></a>
This database contains data from a three-dimensional large-eddy simulation of turbulent flow through a regular array of 81 cubic buildings in 9 rows × 9 columns, of side H = 0.06 m and pitch 2H, reproducing the AIJ Case K (ArraysC) wind tunnel benchmark at model scale (U_H = 2.33 m/s, Re ≈ 9800). Unlike the benchmark, which reports time-averaged velocity and turbulent kinetic energy at 203 probe points, the simulation was run with OpenFOAM (WALE subgrid-scale model, synthetic-turbulence inlet with the measured anisotropic Reynolds stresses), validated against those points, and rescaled by a factor of 400 (H = 24 m, pitch 48 m). The dataset comprises 299 snapshots of pressure and the three velocity components, provided in .vtu (native solver mesh) and .npy (equispaced grid of 205 × 205 × 21 points at Δxy = 2 m, Δz = 5 m, with building mask) formats.

[[Link to EchoNet-Dynamic](https://www.aij.or.jp/%20jpn/publish/cfdguide/index_e.htm)]

## Urban LES database — AIJ Case L (regular 14×9 cubic array)<a id="14x9-cubic-array"></a>
This database contains data from a three-dimensional large-eddy simulation of turbulent flow through a regular array of 126 cubic buildings in 14 rows × 9 columns, of side H = 0.06 m and pitch 2H, reproducing the AIJ Case L (ArraysCT) wind tunnel benchmark at model scale (U_H = 1.34 m/s). Unlike the benchmark, which was conducted under weakly non-isothermal conditions (Rib ≈ −0.04) and reports time-averaged point measurements, the simulation was run isothermally with OpenFOAM (WALE subgrid-scale model, synthetic-turbulence inlet from the measured profile), validated against the benchmark velocities, and rescaled by a factor of 400 (H = 24 m, pitch 48 m). The dataset comprises 299 snapshots of pressure and the three velocity components, provided in .vtu (native solver mesh) and .npy (equispaced grid of 325 × 205 × 21 points at Δxy = 2 m, Δz = 5 m, with building mask) formats.

[[Link to EchoNet-Dynamic](https://www.aij.or.jp/%20jpn/publish/cfdguide/index_e.htm)]

## Urban LES database — AIJ Case M (TPU university campus)<a id="tpu-university-campus"></a>
This database contains data from a three-dimensional large-eddy simulation of turbulent flow over a real university campus in Atsugi (Japan), reproducing the geometry of the AIJ Case M (TPU) wind tunnel benchmark at full scale (domain of about 1080 m × 720 m, tallest building 65 m, terrain elevation included). Unlike the benchmark, which reports time-averaged measurements at sparse points for several wind directions, the simulation was run for a single direction (180°, U_R = 4.08 m/s at H_R = 41 m) with OpenFOAM (WALE subgrid-scale model, synthetic-turbulence inlet from the measured profile) and validated against those measurements. The dataset comprises 450 snapshots of pressure and the three velocity components, provided in .vtu (native solver mesh) and .npy (equispaced grid of 329 × 292 × 21 points at Δxy = 2 m, Δz = 5 m, with building mask) formats.

[[Link to EchoNet-Dynamic](https://www.aij.or.jp/%20jpn/publish/cfdguide/index_e.htm)]
