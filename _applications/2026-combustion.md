---

layout: page
title: "Combustion"
area: "Combustion and reactive flows"
tldr: "Physics-based CFD, reduced-order modelling, and AI-driven prediction for turbulent combustion and reactive flows"
permalink: /software/applications/2026-combustion/
--------------------------------------------------

# Overview

Combustion and reactive-flow modelling combines physics-based simulation, reduced-order modelling, and data-driven prediction to analyse complex reacting systems. This page collects reusable workflows for combustion applications, including OpenFOAM cases, numerical setup guidelines, post-processing scripts, validation examples, and datasets for reduced-order modelling.

The applications focuse on the DLR methane/hydrogen/nitrogen turbulent diffusion flame. The workflow shows how to set up and run a RANS combustion simulation with OpenFOAM `reactingFoam`, validate the temperature field against experimental data, and generate a structured CFD database for reduced-order modelling.

# Index

* [CFD & High-Fidelity Simulations](#cfd)

  * [DLR Flame CFD Workflow](#cfd-workflow)
  * [Tutorial](#cfd-tutorial)
* [AI & Data-Driven Models](#ai)

  * [HOSVD + GPR Parametric Interpolation](#ai-hosvd-gpr)
  * [Tutorial](#hosvd-tutorial-and-post)
* [References](#references)
* [Contributors](#contributors)

# CFD & High-Fidelity Simulations <a id="cfd"></a>

## DLR Flame CFD Workflow <a id="cfd-workflow"></a>

This section provides a reproducible CFD workflow for the DLR turbulent non-premixed jet flame [1]. The burner consists of a central fuel jet containing CH4/H2/N2 and a surrounding dry-air coflow. The fuel is injected through an 8 mm nozzle, while the coflow air is supplied through a 140 mm coaxial nozzle. The geometry is given as follows. An axisymmetric wedge domain is used to reduce the computational cost while preserving the main flame structure and the external ambient region for air entrainment.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/DLR_burner_Geometry.png?raw=true" alt="DLR burner geometry" width="60%">
</p>

The simulation is performed with OpenFOAM-v10 using the `reactingFoam` solver. The case uses:

* a multi-component perfect-gas thermophysical model;
* JANAF thermodynamic data and Sutherland transport;
* the standard `kEpsilon` RANS turbulence model;
* the Eddy Dissipation Concept (EDC) for turbulence-chemistry interaction;
* ODE chemistry integration with `seulex`;
* TDAC acceleration with CH4 and H2 as initiating species;
* blockMesh-based mesh generation and ParaView/OpenFOAM post-processing.

The representative results are given as follows.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/DLR_burner_T_H2_H2O.png?raw=true" alt="Temperature and Mass fractions of H2O and H2" width="70%">
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

## Tutorial <a id="cfd-tutorial"></a>

The complete step-by-step tutorial covering geometry generation, mesh generation, combustion-model setup, solver execution, validation, and post-processing is available here:

* [Tutorial: OpenFOAM RANS simulation of the DLR CH4/H2/N2 turbulent diffusion flame](https://modelflows.github.io/modelflowsapp/software/tutorials/2026-combustion-tutorial/)

# AI & Data-Driven Models <a id="ai"></a>

## Parametric interpolation of DLR turbulent jet diffusion flame using HOSVD + GPR <a id="ai-hosvd-gpr"></a>

Fast predictions of thermochemical variables is one of the necessary steps in making a functional digital twin for reactive flow systems. The framework uses Higher Order Singular Value Decomposition (HOSVD) to reduce the dimensionality of the simulations and Gaussian Process Regression (GPR) to interpolate the behaviour for new combinations of operating parameters.

High-fidelity CFD simulations are at the core of the study and design of combustion systems, but are often too slow and expensive to generate a complete description of the system behaviour across a broad range of operating conditions.

The algorithm works in two stages:

1. Data is decomposed using HOSVD.
2. Gaussian Process Regression is used to interpolate the reduced coefficients.

The intuitive idea is that HOSVD decomposes data as a linear combination of basis modes. Instead of requiring all spatial points of the original CFD solution, the data can be represented as a weighted combination of a limited number of dominant structures. GPR is then used to estimate the modal coefficients corresponding to unseen operating conditions.

## Tutorial <a id="hosvd-tutorial-and-post"></a>
The research post explains the mathematical aspects, while the tutorial provides all implementation details for the dataset described in the previous section.

* [Tutorial: Parametric interpolation of DLR turbulent jet diffusion flame using HOSVD + GPR](https://modelflows.github.io/modelflowsapp/software/tutorials/combustion-hosvd-gpr-tutorial/)

Below a sample of the reconstruction of the temperature field for the flame used in the tutorial:

![Reconstruction of Temperature field for Re=13000, mf=0.08](/assets/img/Tutorial/Combustion/hosvd_gpr/field_T.png)

# Contributors <a id="contributors"></a>

* Isacco Faglioni
* Xiangrui Zou

# References <a id="references"></a>

[*Bergmann, V., Meier, W., Wolff, D., & Stricker, W. (1998). Application of spontaneous Raman and Rayleigh scattering and 2D LIF for the characterization of a turbulent CH4/H2/N2 jet diffusion flame. Applied Physics B, 66(4), 489–502.*](https://doi.org/10.1007/s003400050424)

[*De Lathauwer, L., De Moor, B., & Vandewalle, J. (2000). A multilinear singular value decomposition. SIAM Journal on Matrix Analysis and Applications, 21(4), 1253–1278.*](https://doi.org/10.1137/S0895479896305696)

[*Williams, C. K. I., & Rasmussen, C. E. (1995). Gaussian processes for regression. Advances in Neural Information Processing Systems, 8.*](https://proceedings.neurips.cc/paper/1995/hash/7cce53cf90577442771720a370c3c723-Abstract.html))

[*Barragán, G., Hetherington, A., Abadía-Heredia, R., Garicano-Mena, J., & Le Clainche, S. (2025). HOSVD-SR: A Physics-Based Deep Learning Framework for Super-Resolution in Fluid Dynamics. arXiv:2504.17994.*](https://arxiv.org/abs/2504.17994)

[*Sengupta, A., Abadía-Heredia, R., Hetherington, A., Pérez, J. M., & Le Clainche, S. (2025). Hybrid machine learning models based on physical patterns to accelerate CFD simulations: a short guide on autoregressive models. arXiv:2504.06774.*](https://arxiv.org/abs/2504.06774)
