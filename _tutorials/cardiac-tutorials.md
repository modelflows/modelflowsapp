---
layout: page
title: "Cardiac tutorials for diagnosis and prognosis of cardiovascular diseases (CVD) and CFD"
application: "Cardiac Pathology"
category: "CFD & High-Fidelity Simulations / AI & Data-Driven Models"
tldr: "Tutorials for CFD simulations, and for pattern identification, classification and prediction of cardiovascular diseases"
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
*  [Interface tutorial](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#interface-tutorial)
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

## Interface tutorial <a id="interface-tutorial"></a>

CardioView is the clinical desktop interface that bridges the technical environment; modal decomposition and deep learning models, with the medical environment, letting clinicians load echocardiography videos and run the diagnosis and prognosis models directly, with no coding required. Like large-scale LLMs, the tool also supports automatic retraining on newly validated clinical cases once enough samples are collected.

- [*Codes*](#interface-codes-private)

> #### Codes <a id="interface-codes-private"></a>
> This repository is currently **private** and not yet publicly available. If you are interested in accessing the code, please contact us at [soledad.leclainche@upm.es](mailto:soledad.leclainche@upm.es).

## CFD & High-Fidelity Simulations tutorial <a id="cfd-tutorial"></a>

The full tutorial is available in the Sphinx repository [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/CFD_tutorial):

- Repository: Left Ventricle CFD Simulations

Explore our step-by-step video tutorials on setting up CFD simulations of the left ventricle. These resources include all necessary files to replicate our results, offering a comprehensive guide for anyone aiming to deepen their understanding or reproduce our findings.

### What the tutorial covers

- How to perform geometry pre-processing to define ventricular wall motion required for the simulations.
- How to load the geometry, meshing, and set up the simulation in STAR-CCM+ to replicate left ventricle blood flow results.
- How to perform left ventricle blood flow simulations in Fluent.

### Geometry Pre-Processing

This section provides our MATLAB codes for generating STL file sequences that define ventricular wall motion for CFD simulations. The workflow is based on integrating ventricular volume variation from a flow rate chart that describes the quantity of blood coming in and out of the left ventricle.

We offer two approaches:
* Idealized Geometry: Where the wall motion is defined analytically, and STL files are generated accordingly. 
* Patient-Specific Geometry: Requires code adjustments since analytical expressions are unavailable. This process includes extracting the left ventricle model from cardiotomography data to ensure accurate patient-specific simulations.

Download the necessary files [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/generateSTLFiles.zip).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Slides_Tutorial_GeometryPreprocessing.pptx).

### CFD with Star-CCM+

This section provides a complete guide on replicating our blood flow simulations inside the left ventricle using STAR-CCM+. From loading the geometry and meshing to configuring the simulation settings, we walk you through each step to ensure accurate reproduction of our results.

Download the necessary files [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Tutorial_Star-CCM+.zip).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Slides_Tutorial_StarccmCFD.pptx).

### CFD with Ansys Fluent

In this section, we outline the entire process of setting up blood flow simulations within the left ventricle using Ansys Fluent. From importing the geometry and generating the mesh to configuring the simulation parameters, this guide covers everything needed to successfully replicate our results.

Download the necessary files [*here*](https://drive.upm.es/s/A8EuWtjSuMAetHc).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Slides_Tutorial_FluentCFD.pptx).

### Videos

- **Introduction**: Explanation of the project, integrating CFD simulations with Neural Networks:
<iframe width="560" height="315" src="https://www.youtube.com/embed/XHdfQc7LLgA?si=jY4mia541q-MqgtM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- **Step 1**: Geometry pre-processing:
<iframe width="560" height="315" src="https://www.youtube.com/embed/Bzd_ZniGGG0?si=UvRmu9_2Qd7QxDWJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- **Step 2**: Replicating the blood flow simulations inside the left ventricle using STAR-CCM+:
<iframe width="560" height="315" src="https://www.youtube.com/embed/8YjVIamKzhY?si=U5s0zgmYVJ2fAl5a" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- **Step 3**: Setting up blood flow simulations within the left ventricle using Ansys Fluent, grouping together everything required to successfully replicate the results:
<iframe width="560" height="315" src="https://www.youtube.com/embed/zkAAioOEVDE?si=VAc7JBNCvohALkOS" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### Results

The ideal models of the left ventricle (LV) for our simulations are taken directly from these references and are shown in the following figure. These models essentially represent an idealization of the ventricular cavity with two tubes attached to simulate inflow and outflow through the mitral and aortic valves, respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/geometry_ideal.png?raw=true)

The computational framework used in this study is designed to solve the Navier-Stokes equations, assuming that blood behaves as an incompressible non-Newtonian fluid. We choose laminar flow conditions that are particularly effective in capturing the vortical features of the diastolic phase of the cardiac cycle. Boundary conditions are a critical aspect; therefore, wall motion, inflow and outflow are set to match the ventricular flow rate curve extracted from references. A grid convergence study was performed to ensure that the simulations were fine-tuned.

The primary objective of this study is to examine the formation and evolution of the vortex ring, a prominent flow feature during the E-wave of diastole. The vortex ring plays a pivotal role in cardiac hemodynamics and has been extensively studied in the literature. The vortex ring emerges from the mitral valve during the E-wave of diastole, with its axis aligned with the mitral valve axis. The initial shape of the vortex ring is that of a donut, although it is asymmetric, with a thinner profile closer to the wall. This indicates a healthy heart. As the vortex ring traverses the ventricle, it gradually tilts due to the reduction in inflow velocity. Interactions between the vortex ring and the ventricular walls result in the formation of secondary vortex tubes. These vortex tubes exhibit complex instabilities, which ultimately result in their interaction with the vortex ring and its subsequent destabilization. The evolution of this flow structure is depicted in Figures X and Y for the geometries used by Zheng et al. and Vedula et al., respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Zheng_vorticity.png?raw=true)
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Vedula_vorticity.png?raw=true)

This analysis highlights the importance of CFD in advancing our understanding of intracardiac flow dynamics and developing improved diagnostic and therapeutic strategies for cardiovascular diseases.

### Related links

- Files for geometry pre-processing [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/generateSTLFiles.zip).
- Files for CFD with Star-CCM+ [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Tutorial_Star-CCM+.zip).
- Files for CFD with Ansys Fluent [*here*](https://drive.upm.es/s/A8EuWtjSuMAetHc).
- Application hub: [Cardiac Pathology]({{ "/software/applications/2026-cardiac-pathology/" | relative_url }})

# Contributors

- Andrés Bell-Navas
- Ander Sánchez Muñoz
- Zhuoqun Zhao
- Eneko Lazpita Suinaga
