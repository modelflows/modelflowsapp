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
