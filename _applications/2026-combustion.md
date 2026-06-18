---
layout: page
title: "Combustion"
area: "Combustion and Reactive Flow Modelling"
tldr: "High-fidelity simulations, reduced-order models and data-driven approaches for combustion systems."
---

# Overview

Combustion and reactive-flow modelling combines physics-based simulation, reduced-order modelling, and data-driven prediction to analyse complex reacting systems. This page collects reusable workflows for combustion applications, including OpenFOAM cases, numerical setup guidelines, post-processing scripts, validation examples, and datasets for reduced-order modelling.

The application focuses on the DLR methane/hydrogen/nitrogen turbulent diffusion flame. The workflow shows how to set up and run a RANS combustion simulation with OpenFOAM `reactingFoam`, validate the temperature field against experimental data, and generate a structured CFD database for reduced-order modelling.

# CFD & High-Fidelity Simulations

This section provides a reproducible CFD workflow for the DLR turbulent non-premixed jet flame [1]. The burner consists of a central fuel jet containing CH4/H2/N2 and a surrounding dry-air coflow. The fuel is injected through an 8 mm nozzle, while the coflow air is supplied through a 140 mm coaxial nozzle. The geometry is given as follows. An axisymmetric wedge domain is used to reduce the computational cost while preserving the main flame structure and the external ambient region for air entrainment.

<!-- IMAGES -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/DLR_burner_Geometry.png?raw=true" alt="DLR burner geometry" width="60%">
</p>

The simulation is performed with OpenFOAM-v10 using the `reactingFoam` solver. The case uses:

- a multi-component perfect-gas thermophysical model;
- JANAF thermodynamic data and Sutherland transport;
- the standard `kEpsilon` RANS turbulence model;
- the Eddy Dissipation Concept (EDC) for turbulence-chemistry interaction;
- ODE chemistry integration with `seulex`;
- TDAC acceleration with CH4 and H2 as initiating species;
- blockMesh-based mesh generation and ParaView/OpenFOAM post-processing.

The representive results are given as follows.

<!-- IMAGES -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/DLR_burner_T_H2_H2O.png?raw=true" alt="Temperature and Mass fractions of H2O and H2" width="60%">
</p>

The objective is not only to obtain one flame simulation, but also to provide a reusable workflow for generating CFD datasets. In the current dataset-generation plan, the Reynolds number is varied from 11000 to 20000, and the hydrogen mass fraction is varied from 4% to 22%, producing 100 parametric CFD cases. These solutions can be used to build structured datasets for reduced-order models and data-driven models.

The OpenFOAM workflow covers:

1. geometry and mesh generation with `blockMesh`;
2. fuel, coflow, ambient, outlet, wall, wedge, and axis boundary-condition setup;
3. thermophysical, turbulence, combustion, and chemistry model configuration;
4. solver execution using `reactingFoam`, including parallel execution;
5. post-processing of temperature, velocity, pressure, species, and turbulence fields;
6. validation through radial temperature profiles;
7. organization of CFD outputs for reduced-order modelling.

The full tutorial is available in the following section.
  
# AI & Data-Driven Models

## Parametric interpolation of  DLR turbulent jet diffusion flame using HOSVD + GPR

Fast predictions of thermochemical variables is one of the necessary steps in making a functional digital twin for reactive flowsystems. The framework is to use Higher Order Singular Value Decomposition to reduce the dimensionality of the simulations and Gaussian Process Regression to interpolate the behaviour for new combinations of operating parameters. High fidelity CFD simulations are at the core of the study and design of combustion systems, but are often too slow and expensive to generate a full spectrum of the behaviour of the system for a wide spectrum of operating conditions. 

The algorithm works in two stages: 

1. Data is decomposed using HOSVD
2. Gaussian Process Regression is used to interpolate

The intuitive idea is that HOSVD decomposes data as linear combination of eigenvectors. This means that instead of requiring all "pixels" the data is rewritten as a weighted sum of only a few pictures. The GPR is used to find out how much of each of these pictures is contained in new points that has not been used to build the basis.

The research post explain the mathematical aspects, while the tutorial provide all the details about how to implement the algorithm for the dataset described in the previous seciton. 
- [Tutorial 2: Parametric interpolation of  DLR turbulent jet diffusion flame using HOSVD + GPR](/_tutorials/combustion-hosvd-gpr-tutorial.md)
- [Post: Parametric interpolation of  DLR turbulent jet diffusion flame using HOSVD + GPR](/_posts/combustion-hosvd-gpr.md)

Below a sample of the reoconstruction of the Temperature field for the flame used in the tutorial:
![Reconstruction of Temperature field for Re=13000, mf=0.08](assets/img/Tutorial/Combustion/hosvd_gpr/field_T.png)


# Tutorials

- [Tutorial 1: OpenFOAM RANS simulation of the DLR CH4/H2/N2 turbulent diffusion flame](../_tutorials/2026-combustion_tutorial.md)
- [Tutorial 2: Parametric interpolation of  DLR turbulent jet diffusion flame using HOSVD + GPR](/_tutorials/combustion-hosvd-gpr-tutorial.md)


- Name: Isacco Faglioni
- Name: Xiangrui Zou


<!-- REFERENCES -->
[*Bergmann, V., Meier, W., Wolff, D., & Stricker, W. (1998). Application of spontaneous Raman and Rayleigh scattering and 2D LIF for the characterization of a turbulent CH4/H2/N2 jet diffusion flame. Applied Physics B, 66(4), 489-502.*](https://doi.org/10.1007/s003400050424)

