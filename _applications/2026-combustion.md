---
layout: page
title: "Combustion"
area: "Combustion and Reactive Flow Modelling"
tldr: "High-fidelity simulations, reduced-order models and data-driven approaches for combustion systems."
---

# Overview

Combustion and reactive-flow modelling combines physics-based simulation, reduced-order modelling, and data-driven prediction to analyse complex reacting systems. This page collects reusable workflows for combustion applications, including OpenFOAM cases, numerical setup guidelines, post-processing scripts, validation examples, and datasets for reduced-order modelling.

The first example focuses on the DLR methane/hydrogen/nitrogen turbulent diffusion flame. The workflow shows how to set up and run a RANS combustion simulation with OpenFOAM `reactingFoam`, validate the temperature field against experimental data, and generate a structured CFD database for tensor-based reduced-order modelling.

# CFD & High-Fidelity Simulations

## DLR CH4/H2/N2 turbulent diffusion flame with OpenFOAM

This example provides a reproducible CFD workflow for the DLR turbulent non-premixed jet flame [1]. The burner consists of a central fuel jet containing CH4/H2/N2 and a surrounding dry-air coflow. The fuel is injected through an 8 mm nozzle, while the coflow air is supplied through a 140 mm coaxial nozzle. An axisymmetric wedge domain is used to reduce the computational cost while preserving the main flame structure and the external ambient region for air entrainment.

The simulation is performed with OpenFOAM-v10 using the `reactingFoam` solver. The case uses:

- a multi-component perfect-gas thermophysical model;
- JANAF thermodynamic data and Sutherland transport;
- the standard `kEpsilon` RANS turbulence model;
- the Eddy Dissipation Concept (EDC) for turbulence-chemistry interaction;
- ODE chemistry integration with `seulex`;
- TDAC acceleration with CH4 and H2 as initiating species;
- blockMesh-based mesh generation and ParaView/OpenFOAM post-processing.

The objective is not only to obtain one flame simulation, but also to provide a reusable workflow for generating CFD datasets. In the current dataset-generation plan, the Reynolds number is varied from 11000 to 20000, and the hydrogen mass fraction is varied from 4% to 22%, producing 100 parametric CFD cases. These solutions can be used to build structured datasets for reduced-order models and data-driven models.

The OpenFOAM workflow covers:

1. geometry and mesh generation with `blockMesh`;
2. fuel, coflow, ambient, outlet, wall, wedge, and axis boundary-condition setup;
3. thermophysical, turbulence, combustion, and chemistry model configuration;
4. solver execution using `reactingFoam`, including parallel execution;
5. post-processing of temperature, velocity, pressure, species, and turbulence fields;
6. validation through radial temperature profiles;
7. organization of CFD outputs for reduced-order modelling.

The full tutorial is available here:

- [Tutorial 1: OpenFOAM RANS simulation of the DLR CH4/H2/N2 turbulent diffusion flame](./2026-combustion_tutorial.md)
  
# AI & Data-Driven Models

Add here POD, DMD, HODMD, ROMs, machine learning, deep learning, prediction, reconstruction, classification, or data assimilation workflows.

# Tutorials

- [Tutorial 1: OpenFOAM RANS simulation of the DLR CH4/H2/N2 turbulent diffusion flame](./2026-combustion_tutorial.md)
- Tutorial 2:

# Notebooks

- Notebook 1:
- Notebook 2:

# Videos

- Video 1:
- Video 2:

# Resources & Databases

- Dataset:
- Case files:
- Mesh:
- Simulation outputs:

# Publications

- Paper / preprint / related post:

# Contributors

- Name:


<!-- REFERENCES -->
[*Bergmann, V., Meier, W., Wolff, D., & Stricker, W. (1998). Application of spontaneous Raman and Rayleigh scattering and 2D LIF for the characterization of a turbulent CH4/H2/N2 jet diffusion flame. Applied Physics B, 66(4), 489-502.*](https://doi.org/10.1007/s003400050424)

