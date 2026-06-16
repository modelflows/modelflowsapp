---
layout: page
title: "Urban Flows"
area: "Urban Flow Modelling"
tldr: "CFD simulations, air-quality analysis, reduced-order modelling and data-driven methods for urban environments."
---

# Overview

Briefly describe the application, motivation, physical problem, available data, and expected learning outcomes.

# CFD & High-Fidelity Simulations

Add here geometry generation, meshing, boundary conditions, solver setup, OpenFOAM cases, post-processing workflows, and high-fidelity simulations.

## Tutorials
- [Urban CFD Workflow (Sphinx Tutorial)]({{ "/software/tutorials/urban-cfd/" | relative_url }})
- [Urban CFD Workflow]({{ "/software/tutorials/urban-cfd/" | relative_url }})
- Tutorial 3:

# AI, ROM & Data-Driven Models

This part collects the reduced-order modelling and data-driven workflows developed for urban flow and air-pollution applications. The objective is to connect sparse sensor information, high-fidelity CFD data, reduced-order models, temporal prediction methods, and low-cost sensor calibration into a common scientific workflow.

The AI/ROM part is organized into three main directions:

1. **3D reconstruction from sparse sensors**  
   Reconstruction of full 3D urban flow and pollutant fields from a reduced number of sensor locations using low-cost modal decomposition methods.

2. **Temporal prediction of urban flow fields**  
   Forecasting of future flow and pollutant states using multidimensional modal decomposition and data-driven temporal models.

3. **Calibration of low-cost air-quality sensors**  
   Correction of low-cost sensor measurements using temporal deep learning models trained with reference-grade observations.

---

## 3D Reconstruction from Sparse Sensors

This workflow focuses on recovering full 3D urban flow and pollutant fields from sparse sensor information. The goal is to reduce the storage and computational cost of high-fidelity CFD datasets while preserving the dominant spatial structures of the original field.

The reconstruction methods include:

- **lcSVD**: low-cost matrix-based reconstruction using sparse sensor measurements;
- **lcHOSVD**: low-cost tensor-based reconstruction that preserves the 3D spatial structure;
- **lcHODMD**: low-cost higher-order dynamic mode decomposition for reconstructing and analysing time-dependent flow structures from reduced data.

These methods are designed for variables such as velocity components, pressure, turbulent quantities, and pollutant concentrations.

### Related Research Page

- [From Sensors to 3D Reconstruction]({{ "/research/ai-models/ai-urban-flows/2026-from-sensors-to-3d-reconstruction/" | relative_url }})

### Tutorials

- [Urban Sensors 3D Reconstruction]({{ "/software/tutorials/urban-sensors3drec/" | relative_url }})
- lcROMs reconstruction tutorial: coming soon
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

---

## Temporal Prediction of Urban Flow Fields

This workflow focuses on predicting the temporal evolution of urban flow and pollutant fields. The objective is to build reduced-order temporal models that can forecast future states without rerunning the full CFD simulation.

The prediction methods include:

- **mdHODMD**: multidimensional higher-order dynamic mode decomposition for extracting spatial-temporal coherent structures;
- **iterative temporal prediction**: forecasting future flow snapshots from reduced modal dynamics;
- **sequence-based learning models**: deep-learning models such as LSTM can be combined with reduced modal coefficients for data-driven forecasting.

This direction is intended for fast prediction of velocity fields, pressure fields, and pollutant concentration distributions in urban domains.

### Related Research Page

- mdHODMD-based urban flow prediction: coming soon

### Tutorials

- mdHODMD prediction tutorial: coming soon
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

---

## Calibration of Low-Cost Air-Quality Sensors

This workflow focuses on improving the reliability of low-cost air-quality sensor measurements. Low-cost sensors are useful for dense urban monitoring, but their raw measurements are affected by drift, environmental sensitivity, and device-to-device variability.

The calibration framework uses temporal deep learning to correct low-cost sensor data using:

- co-located reference measurements;
- meteorological variables;
- lagged sensor features;
- harmonic time encodings;
- interaction terms;
- rolling-window sequence generation;
- LSTM-based calibration models.

The current calibration work focuses on PM2.5, PM10, and NO2 using low-cost sensor data from the OxAria network.

### Related Research Page

- [Temporal Deep Learning Calibration of Low-Cost Air Quality Sensors]({{ "/research/ai-models/air-pollution/2026-temporal-deep-learning-calibration-low-cost-sensors/" | relative_url }})

### Tutorials

- Low-cost sensor calibration tutorial: coming soon
- LSTM calibration notebook: coming soon

## Tutorials
- [Urban Sensors 3D Reconstruction]({{ "/software/tutorials/urban-sensors3drec/" | relative_url }})
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
