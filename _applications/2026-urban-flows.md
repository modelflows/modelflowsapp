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
  - [Urban CFD with OpenFOAM: 9 buildings canonical configuration](#urban-cfd-with-openfoam-aij-case-c)

- [AI, ROM & Data-Driven Models](#ai-rom--data-driven-models)
  - [3D Reconstruction from Sparse Sensors](#1-3d-reconstruction-from-sparse-sensors)
  - [Temporal Prediction of Urban Flow Fields](#2-temporal-prediction-of-urban-flow-fields)
  - [Calibration of Low-Cost Air-Quality Sensors](#3-calibration-of-low-cost-air-quality-sensors)

- [Publications](#publications)
- [Contributors](#contributors)

# CFD & High-Fidelity Simulations

This section includes workflows related to geometry generation, meshing, boundary conditions, solver setup, OpenFOAM cases, and post-processing for high-fidelity urban flow simulations.

## Urban CFD with OpenFOAM: 9 buildings canonical configuration

## Introduction

This section covers the canonical configuration of the 9 buildings in an urban CFD simulation workflow using OpenFOAM, including geometry preparation, OpenFOAM case setup, simulation, and post-processing, applied to a simplified urban flow system. The test case is a 3x3 array of square cylinders (buildings), each 0.2 m high by 0.2 m long by 0.2 m deep, with a distance between each of them of 0.2 m. This layout mimics the AIJ Case C wind tunnel benchmarks.

To allow the wind direction to be varied without re-meshing, the workflow uses a cylindrical computational domain, following the domain-sizing best practices of Blocken (2015). On this domain, a single mesh and case setup can be reused across a full range of flow conditions, from geometry generation in Blender through meshing, solving, and analysis of the resulting flow field.

- Tutorial: *Coming soon...*


# AI, ROM & Data-Driven Models

This section presents the tutorials combining Artificial Intelligence, Reduced-Order Modelling and Modal Decomposition for urban flow and air-pollution applications. These methods are used to reconstruct high-dimensional CFD fields from sparse sensor information, predict future flow and pollutant states, and calibrate low-cost air-quality sensor measurements.

## 1. 3D Reconstruction from Sparse Sensors

This topic focuses on the reconstruction of full 3D urban flow and pollutant fields from a reduced number of sensor locations. Low-cost modal decomposition methods, such as lcSVD and lcHOSVD, are used to recover the original high-dimensional CFD fields while reducing the amount of data required for reconstruction.

The complete step-by-step tutorial is available in the <a href="{{ '/software/tutorials/urban-3d-reconstruction/' | relative_url }}">Urban Sensors 3D Reconstruction</a> page. This link goes to the workflow explaining sparse-sensor selection, low-cost decomposition, field reconstruction, error evaluation and comparison with the original CFD solution.

The related research page is available here: <a href="{{ '/research/ai-models/ai-urban-flows/2026-from-sensors-to-3d-reconstruction/' | relative_url }}">From Sensors to 3D Reconstruction</a>. This link goes to the research summary describing the motivation, methodology, datasets and reconstruction results for the low-cost 3D reconstruction work.

## 2. Temporal Prediction of Urban Flow Fields

This topic focuses on the prediction of future urban flow and pollutant states from time-resolved CFD databases. Multidimensional modal decomposition and deep learning models are used to learn the temporal evolution of the flow field and reconstruct the predicted snapshots.

The complete step-by-step tutorial is available in the <a href="{{ '/software/tutorials/urban-mdhodmd-forecasting/' | relative_url }}">Temporal Prediction of Urban Flow Fields</a> page. This link goes to the workflow explaining data normalization, modal decomposition, sequence preparation, temporal learning and autoregressive prediction.

The related research page will be added soon.

## 3. Calibration of Low-Cost Air-Quality Sensors

This topic focuses on the calibration of low-cost air-quality sensors using temporal deep learning models. The objective is to correct raw low-cost sensor measurements by learning their relationship with reference-grade observations, meteorological variables and temporal dependencies.

The complete step-by-step tutorial is available in the <a href="{{ '/software/tutorials/urban-lcs-calibration/' | relative_url }}">Low-Cost Sensor Calibration</a> page. This link goes to the workflow explaining data cleaning, feature preparation, temporal sequence generation, LSTM model training and calibrated sensor output.

The related research page is available here: <a href="{{ '/research/ai-models/air-pollution/2026-temporal-deep-learning-calibration-low-cost-sensors/' | relative_url }}">Temporal Deep Learning Calibration of Low-Cost Air Quality Sensors</a>. This link goes to the research summary and paper information for the low-cost sensor calibration study.

## Notebooks

- <a href="https://github.com/modelflows/notebooks/tree/main/LCS%20calibration">Low-Cost Sensor Calibration Notebook</a>: this link goes to the notebook implementing the temporal deep learning calibration framework for low-cost air-quality sensors.
- 3D Reconstruction Notebook: coming soon.
- Temporal Prediction Notebook: coming soon.

## Resources & Databases

- Dataset for low-cost sensor calibration: <a href="http://ora.ox.ac.uk/objects/uuid:66fbe8c1-4b63-4124-bf0d-a78cbc9e1408">OxAria low-cost air-quality sensor dataset</a>. This link goes to the open-access dataset used for the low-cost sensor calibration study.
- Dataset for 3D reconstruction: coming soon.
- Dataset for temporal prediction: coming soon.

# Publications

Further details about the low-cost sensor calibration application can be found in the following reference:

- <a href="https://doi.org/10.48550/arXiv.2604.21527">Sengupta, A., Bush, T., Marner, B., Pérez, J. M., & Le Clainche, S. (2026). A Temporal Deep Learning Framework for Calibration of Low-Cost Air Quality Sensors. arXiv:2604.21527 [cs.LG].</a>

Further publications related to urban flow reconstruction and temporal prediction will be added soon.

# Contributors

- Arindam Sengupta
- Paul Jeanney
- Guillermo Enrique Barragan Montalvo
- Alberto Rodriguez Fernandez
- Wentai Deng
  
