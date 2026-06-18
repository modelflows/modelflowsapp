---
layout: page
title: "Urban Flows"
area: "Urban Flow Modelling"
tldr: "CFD simulations, air-quality analysis, reduced-order modelling and data-driven methods for urban environments."
---

# Overview

This application page collects the main workflows developed for urban flow and air-quality applications within ModelFLOWs. The objective is to provide a common entry point for CFD simulations, high-fidelity data generation, reduced-order modelling, temporal prediction, sparse-sensor reconstruction, and low-cost air-quality sensor calibration.

The page is organized as an index. Each topic below links to the corresponding tutorial or research page, where the detailed methodology, notebooks, datasets, videos, and additional resources are provided.

# Index

- [CFD & High-Fidelity Simulations](#cfd--high-fidelity-simulations)
  - [Urban CFD with OpenFOAM: AIJ Case C](#urban-cfd-with-openfoam-aij-case-c)

- [AI, ROM & Data-Driven Models](#ai-rom--data-driven-models)
  - [3D Reconstruction from Sparse Sensors](#1-3d-reconstruction-from-sparse-sensors)
  - [Temporal Prediction of Urban Flow Fields](#2-temporal-prediction-of-urban-flow-fields)
  - [Calibration of Low-Cost Air-Quality Sensors](#3-calibration-of-low-cost-air-quality-sensors)

- [Publications](#publications)
- [Contributors](#contributors)

# CFD & High-Fidelity Simulations

This section includes workflows related to geometry generation, meshing, boundary conditions, solver setup, OpenFOAM cases, and post-processing for high-fidelity urban flow simulations.

## Urban CFD with OpenFOAM: AIJ Case C

This topic covers the canonical urban CFD workflow, including geometry preparation, OpenFOAM case setup, simulation, and post-processing.

- Tutorial: <a href="{{ '/tutorials/urban-canonical-configuration/' | relative_url }}">Urban CFD with OpenFOAM: AIJ Case C</a>

# AI, ROM & Data-Driven Models

This section collects the reduced-order modelling and data-driven workflows developed for urban flow and air-pollution applications. The objective is to connect sparse sensor information, high-fidelity CFD data, reduced-order models, temporal prediction methods, and low-cost sensor calibration into a common scientific workflow.

## 1. 3D Reconstruction from Sparse Sensors

This topic focuses on the reconstruction of full 3D urban flow and pollutant fields from a reduced number of sensor locations using low-cost modal decomposition methods.

- Research page: <a href="{{ '/research/ai-models/ai-urban-flows/2026-from-sensors-to-3d-reconstruction/' | relative_url }}">From Sensors to 3D Reconstruction</a>
- Tutorial: <a href="{{ '/software/tutorials/urban-3d-reconstruction/' | relative_url }}">Urban Sensors 3D Reconstruction</a>

## 2. Temporal Prediction of Urban Flow Fields

This topic focuses on the prediction of future urban flow and pollutant states using multidimensional modal decomposition and data-driven temporal models.

- Research page: coming soon
- Tutorial: <a href="{{ '/software/tutorials/urban-mdhodmd-forecasting/' | relative_url }}">Temporal Prediction of Urban Flow Fields</a>

## 3. Calibration of Low-Cost Air-Quality Sensors

This topic focuses on the correction of low-cost air-quality sensor measurements using temporal deep learning models trained with reference-grade observations.

- Research page: <a href="{{ '/research/ai-models/air-pollution/2026-temporal-deep-learning-calibration-low-cost-sensors/' | relative_url }}">Temporal Deep Learning Calibration of Low-Cost Air Quality Sensors</a>
- Tutorial: <a href="{{ '/software/tutorials/urban-lcs-calibration/' | relative_url }}">Calibration of Low-Cost Air-Quality Sensors</a>

# Publications

- <a href="https://doi.org/10.48550/arXiv.2604.21527">Sengupta, A., Bush, T., Marner, B., Pérez, J. M., & Le Clainche, S. (2026). A Temporal Deep Learning Framework for Calibration of Low-Cost Air Quality Sensors. arXiv:2604.21527 [cs.LG].</a>

# Contributors

- Arindam Sengupta
- Paul Jeanney
- Alberto Rodriguez Fernanadez
- Tony Bush
- Ben Marner
- José Miguel Pérez
- Soledad Le Clainche
