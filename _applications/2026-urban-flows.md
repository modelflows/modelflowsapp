---
layout: page
title: "Urban Flows"
area: "Urban Flow Modelling"
tldr: "CFD simulations, air-quality analysis, reduced-order modelling and data-driven methods for urban environments."
---

# Overview

This section concerns methods addressing several tasks related to the study of urban flows and air quality: high-fidelity CFD simulations, sparse-sensor reconstruction, temporal prediction of flow and pollutant fields, and calibration of low-cost air-quality sensors. Modal decomposition, reduced-order modelling and deep learning architectures are used together with CFD databases and sensor measurements.

# Index

* [CFD & High-Fidelity Simulations](#cfd)
  * [Required tools and software](#cfd-required-software)
  * [Tutorial](#cfd-tutorials)
* [AI & Data-Driven Models](#ai)
  * [3D Reconstruction Tutorial](#ai-reconstruction)
  * [Temporal Prediction Tutorial](#ai-prediction)
  * [Low-Cost Sensor Calibration Tutorial](#ai-calibration)
  * [Notebooks](#ai-notebooks)
  * [Resources & Databases](#ai-resources)
* [Publications](#publications)
* [Contributors](#contributors)

# CFD & High-Fidelity Simulations <a id="cfd"></a>

Computational Fluid Dynamics (CFD) is used to generate high-fidelity urban flow and pollutant dispersion databases. These simulations provide detailed information about the interaction between buildings, street canyons, wake regions, recirculation zones and pollutant transport. The resulting databases are then used for post-processing, visualization, reduced-order modelling and data-driven analysis.

## Required tools and software <a id="cfd-required-software"></a>

* [OpenFOAM](https://www.openfoam.com/)
* [ParaView](https://www.paraview.org/)
* [Python](https://www.python.org/)
* [NumPy](https://numpy.org/)
* [Matplotlib](https://matplotlib.org/)
* [PyVista](https://pyvista.org/)

## Tutorial <a id="cfd-tutorials"></a>

The complete step-by-step tutorial for the canonical urban CFD case is available in the [*Urban CFD with OpenFOAM: AIJ Case C*]({{ "/tutorials/urban-canonical-configuration/" | relative_url }}) tutorial. This link goes to the workflow for setting up and analysing an urban CFD benchmark configuration, including the simulation case and post-processing steps.

# AI & Data-Driven Models <a id="ai"></a>

This section presents the tutorials combining Artificial Intelligence, Reduced-Order Modelling and Modal Decomposition for urban flow and air-pollution applications. These methods are used to reconstruct high-dimensional CFD fields from sparse sensor information, predict future flow states, and calibrate low-cost air-quality sensor measurements.

## 3D Reconstruction Tutorial <a id="ai-reconstruction"></a>

This tutorial focuses on the reconstruction of full 3D urban flow and pollutant fields from a reduced number of sensor locations. Low-cost modal decomposition methods, such as lcSVD and lcHOSVD, are used to recover the original high-dimensional CFD fields while reducing storage and computational cost.

The complete tutorial is available in the [*Urban Sensors 3D Reconstruction*]({{ "/software/tutorials/urban-3d-reconstruction/" | relative_url }}) page.

The related research page is available here: [*From Sensors to 3D Reconstruction*]({{ "/research/ai-models/ai-urban-flows/2026-from-sensors-to-3d-reconstruction/" | relative_url }}).

## Temporal Prediction Tutorial <a id="ai-prediction"></a>

This tutorial focuses on the temporal prediction of urban flow and pollutant fields. Multidimensional modal decomposition and deep learning models are used to predict the future evolution of time-resolved CFD databases.

The complete tutorial is available in the [*Temporal Prediction of Urban Flow Fields*]({{ "/software/tutorials/urban-mdhodmd-forecasting/" | relative_url }}) page.

The related research page will be added soon.

## Low-Cost Sensor Calibration Tutorial <a id="ai-calibration"></a>

This tutorial focuses on the calibration of low-cost air-quality sensors using temporal deep learning models. The objective is to correct raw low-cost sensor measurements by learning their relationship with reference-grade observations and meteorological variables.

The complete tutorial is available in the [*Low-Cost Sensor Calibration*]({{ "/software/tutorials/urban-lcs-calibration/" | relative_url }}) page.

The related research page is available here: [*Temporal Deep Learning Calibration of Low-Cost Air Quality Sensors*]({{ "/research/ai-models/air-pollution/2026-temporal-deep-learning-calibration-low-cost-sensors/" | relative_url }}).

## Notebooks <a id="ai-notebooks"></a>

- [*Low-Cost Sensor Calibration Notebook*](https://github.com/modelflows/notebooks/tree/main/LCS%20calibration): this link goes to the source files and notebooks implementing the temporal deep learning calibration framework for low-cost air-quality sensors.
- *3D Reconstruction Notebook*: coming soon.
- *Temporal Prediction Notebook*: coming soon.

## Resources & Databases <a id="ai-resources"></a>

- Dataset for low-cost sensor calibration: [*OxAria low-cost air-quality sensor dataset*](http://ora.ox.ac.uk/objects/uuid:66fbe8c1-4b63-4124-bf0d-a78cbc9e1408). This link goes to the open-access dataset used for the low-cost sensor calibration study.
- Dataset for 3D reconstruction: coming soon.
- Dataset for temporal prediction: coming soon.

# Publications <a id="publications"></a>

Further details about the low-cost sensor calibration application can be found in the following reference:

- [*Sengupta, A., Bush, T., Marner, B., Pérez, J. M., & Le Clainche, S. (2026). A Temporal Deep Learning Framework for Calibration of Low-Cost Air Quality Sensors. arXiv:2604.21527 [cs.LG].*](https://doi.org/10.48550/arXiv.2604.21527)

Further publications related to urban flow reconstruction and temporal prediction will be added soon.

# Contributors <a id="contributors"></a>

- Arindam Sengupta
- Paul Jeanney
- Alberto Rodriguez Fernanadez
- Tony Bush
- Ben Marner
- José Miguel Pérez
- Soledad Le Clainche
