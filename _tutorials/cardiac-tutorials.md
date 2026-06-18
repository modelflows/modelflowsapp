---
layout: page
title: "Diagnosis and prognosis of cardiovascular diseases (CVD)"
application: "Cardiac Pathology"
category: "AI & Data-Driven Models"
tldr: "Tutorials for pattern identification, classification and prediction of cardiovascular diseases"
author: "Andrés Bell-Navas"
sphinx_repository: "https://github.com/modelflows/ModelFLOWs-cardiac"
tutorial_file: "TUTORIAL.md"
---

# Overview

This page links to the tutorials of all applications for recognition of cardiovascular diseases by analysing medical and CFD data.

# Tutorials

All tutorials are available [*here*](https://github.com/modelflows/ModelFLOWs-cardiac).

Content:

*  [Diagnosis tutorial](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#diagnosis-tutorial)
*  [Prognosis tutorial](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#prognosis-tutorial)
*  [CFD tutorial](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#cfd-tutorial)

## Diagnosis tutorial <a id="diagnosis-tutorial"></a>

The full tutorial is available in the Sphinx repository [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/diagnosis_tutorial):

- Repository: AI-Based Cardiac Diagnosis from Echocardiography
- [*Diagnosis Tutorial*](https://github.com/modelflows/ModelFLOWs-cardiac/blob/main/diagnosis_tutorial/TUTORIAL.md)
- [*Documentation page*](https://github.com/modelflows/ModelFLOWs-cardiac/blob/main/diagnosis_tutorial/docs/index.md)

### What the tutorial covers

- How to organise the echocardiography datasets.
- How to run normalisation.
- (Optional) how to apply HODMD pre-processing.
- How to pre-train Masked Autoencoder (MAE).
- How to train the ViT classifier.
- How to evaluate the performance on new echocardiography datasets and inspect the results.

### Related links

- [*Notebooks*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/diagnosis_tutorial/notebooks)
- Datasets: Confidential CNIC datasets. 
- Application hub: [Cardiac Pathology]({{ "/software/applications/2026-cardiac-pathology/" | relative_url }})

## Prognosis tutorial <a id="prognosis-tutorial"></a>

The full tutorial is available in the Sphinx repository [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/prognosis_tutorial):

- Repository: AI-Based Cardiac Prognosis from Echocardiography
- [*Prognosis Tutorial*](https://github.com/modelflows/ModelFLOWs-cardiac/blob/main/prognosis_tutorial/TUTORIAL.md)
- [*Documentation page*](https://github.com/modelflows/ModelFLOWs-cardiac/blob/main/prognosis_tutorial/docs/index.md)

### What the tutorial covers

- How to organise the echocardiography datasets.
- How to run normalisation.
- (Optional) how to apply HODMD pre-processing.
- How to pre-train Masked Autoencoder (MAE).
- How to train the ViT regression model.
- How to evaluate the performance on new echocardiography datasets and inspect the results.

### Related links

- [*Notebooks*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/prognosis_tutorial/notebooks)
- Datasets: Confidential CNIC datasets.
- Application hub: [Cardiac Pathology]({{ "/software/applications/2026-cardiac-pathology/" | relative_url }})

## CFD & High-Fidelity Simulations tutorial <a id="cfd-tutorial"></a>

The full tutorial is available in the Sphinx repository [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/CFD_tutorial):

- Repository: Left Ventricle CFD Simulations

### What the tutorial covers

- How to perform geometry pre-processing to define ventricular wall motion required for the simulations.
- How to load the geometry, meshing, and set up the simulation in STAR-CCM+ to replicate left ventricle blood flow results.
- How to perform left ventricle blood flow simulations in Fluent.

### Related links

- Necessary files [*here*](https://drive.upm.es/s/A8EuWtjSuMAetHc).
- Video: 
<iframe width="560" height="315" src="https://www.youtube.com/embed/XHdfQc7LLgA?si=jY4mia541q-MqgtM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
- Application hub: [Cardiac Pathology]({{ "/software/applications/2026-cardiac-pathology/" | relative_url }})

# Contributors

- Andrés Bell-Navas
- Ander Sánchez
- Zhuoqun Zhao
