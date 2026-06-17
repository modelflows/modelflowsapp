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
- [Urban CFD with OpenFOAM: AIJ Case C]({{ "/tutorials/urban-canonical-configuration/" | relative_url }})

# AI, ROM & Data-Driven Models

This part collects the reduced-order modelling and data-driven workflows developed for urban flow and air-pollution applications. The objective is to connect sparse sensor information, high-fidelity CFD data, reduced-order models, temporal prediction methods, and low-cost sensor calibration into a common scientific workflow.

The AI/ROM part is organized into:

# 1. **3D reconstruction from sparse sensors**  
   Reconstruction of full 3D urban flow and pollutant fields from a reduced number of sensor locations using low-cost modal decomposition methods.

### Related Research Page

- <a href="{{ '/research/ai-models/ai-urban-flows/2026-from-sensors-to-3d-reconstruction/' | relative_url }}">From Sensors to 3D Reconstruction</a>

### Tutorials

- <a href="{{ '/software/tutorials/urban-3d-reconstruction/' | relative_url }}">Urban Sensors 3D Reconstruction</a>
### Notebooks

- Notebook 1: coming soon

### Videos

- Video 1: coming soon


### Resources & Databases

- Dataset: coming soon
- Case files: coming soon


### Publications

- Paper / preprint / related post: coming soon

### Contributors

- Arindam Sengupta
- Paul Jeanney
- José Miguel Pérez
- Soledad Le Clainche
  

# 2. **Temporal prediction of urban flow fields**  
   Forecasting of future flow and pollutant states using multidimensional modal decomposition and data-driven temporal models.
### Related Research Page

- mdHODMD-based urban flow prediction: coming soon

### Tutorials

- <a href="{{ '/software/tutorials/urban-mdhodmd-forecasting/' | relative_url }}">Predictions</a>

### Notebooks

- Notebook 1:coming soon


### Videos

- Video 1:coming soon


### Resources & Databases

- Dataset:coming soon
- Case files:coming soon

### Publications

- Paper / preprint / related post:coming soon

### Contributors

- Arindam Sengupta
- José Miguel Pérez
- Soledad Le Clainche


# 3. **Calibration of low-cost air-quality sensors**  
   Correction of low-cost sensor measurements using temporal deep learning models trained with reference-grade observations.
### Related Research Page

- <a href="{{ '/research/ai-models/air-pollution/2026-temporal-deep-learning-calibration-low-cost-sensors/' | relative_url }}">Temporal Deep Learning Calibration of Low-Cost Air Quality Sensors</a>

### Tutorials

- <a href="{{ '/software/tutorials/urban-lcs-calibration/' | relative_url }}">Low-cost sensor calibration tutorial</a>

### Notebooks

- Notebook 1: coming soon

### Videos

- Video 1:


### Resources & Databases

- Dataset:coming soon
- Case files:coming soon

### Publications

- Paper / preprint / related post: Arindam Sengupta, Tony Bush, Ben Marner, Jose Miguel Pérez, and Soledad Le Clainche.  
**A Temporal Deep Learning Framework for Calibration of Low-Cost Air Quality Sensors.**  
arXiv:2604.21527 [cs.LG], 2026.  
[https://doi.org/10.48550/arXiv.2604.21527](https://doi.org/10.48550/arXiv.2604.21527)


### Contributors

- Arindam Sengupta
- Tony Bush
- Ben Marner
- José Miguel Pérez
- Soledad Le Clainche

---







