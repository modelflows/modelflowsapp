---
layout: page
title: "Cardiac Pathology"
area: "Cardiovascular Modelling and Diagnosis"
tldr: "Patient-specific CFD, medical data analysis, reduced-order modelling and AI-based pathology identification."
---

# Overview

This section concerns methods addressing several tasks related with the study of cardiovascular diseases (CVDs): pattern identification, diagnosis and prognosis Modal decomposition and deep learning architectures are used, and also cardiac flow simulations are generated. For this purpose, medical data and CFD databases are used.

# Index

* [CFD & High-Fidelity Simulations](#cfd)
  * [Required tools and software](#cfd-required-software)
  * [Tutorial](#cfd-tutorials)
* [AI & Data-Driven Models](#ai)
  * [Diagnosis & Prognosis Tutorial](#ai-tutorials)
  * [Interface Tutorial](#ai-interface)
  * [Notebooks](#ai-notebooks)
  * [Resources & Databases](#ai-resources)
* [Publications](#publications)
* [Contributors](#contributors)

# CFD & High-Fidelity Simulations <a id="cfd"></a>

Computational Fluid Dynamics (CFD) has emerged as a key tool for modeling the intricate dynamics of intracardiac blood flow. This approach not only enhances our fundamental understanding of cardiac function, but also paves the way for innovative treatment strategies.

## Required tools and software <a id="cfd-required-software"></a>

* [Matlab](https://es.mathworks.com/products/matlab.html)
* [Spyder](https://www.spyder-ide.org/)
* [Star-CCM+](https://plm.sw.siemens.com/en-US/simcenter/fluids-thermal-simulation/star-ccm/?srsltid=AfmBOoqvQTHcTwcvPnM1Fc9M8LCw2NWBRd50mWwnrLL_ZBjIjw5h8dR0)
* [Ansys Fluent](https://www.ansys.com/products/fluids/ansys-fluent)
* [3D Slicer](https://www.slicer.org/)
* [MeshLab](https://www.meshlab.net/)
* [ParaView](https://www.paraview.org/)
* [CT Scans](https://figshare.com/s/2a5de3a2b89a3fb87932?file=5011837)

## Tutorial <a id="cfd-tutorials"></a>

The complete step-by-step tutorial — geometry pre-processing, simulation setup in STAR-CCM+ and Ansys Fluent, downloadable files/slides, video guides and results — is available in the [*CFD tutorial*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#cfd-tutorial) section of the [*Cardiac tutorials*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/) page.

# AI & Data-Driven Models <a id="ai"></a>

This section presents the tutorials to use the methods combining Artificial Intelligence and Modal Decomposition for pattern identification, diagnosis and prognosis of cardiovascular diseases.

## Diagnosis & Prognosis Tutorial <a id="ai-tutorials"></a>

The complete step-by-step tutorials are available in the [*Diagnosis tutorial*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#diagnosis-tutorial) and [*Prognosis tutorial*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#prognosis-tutorial) sections of the [*Cardiac tutorials*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/) page.

## Interface Tutorial <a id="ai-interface"></a>

CardioView is a clinical desktop interface that bridges the technical modelling environment with the medical environment, letting clinicians load echocardiography videos and run the diagnosis and prognosis models directly, with no coding required. As with large-scale LLMs, the tool also supports automatic retraining on newly validated clinical cases once enough samples are collected, keeping the underlying models up to date with real-world data.

The complete tutorial is available in the [*Interface tutorial*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/#interface-tutorial) section of the [*Cardiac tutorials*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/) page.

## Notebooks <a id="ai-notebooks"></a>

- [*Diagnosis Notebooks*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/diagnosis_tutorial/notebooks): this link goes to the source files and to the guide of how to use the codes implementing the training and testing of models for the diagnosis of cardiovascular diseases (CVD).
- [*Prognosis Notebooks*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/prognosis_tutorial/notebooks): this link goes to the source files and to the guide of how to use the codes implementing the training and testing of models for the prognosis of heart failures.

## Resources & Databases <a id="ai-resources"></a>

- Dataset: confidential CNIC datasets.

# Publications <a id="publications"></a>

For validation of the CFD simulations, we base our study on the work of Zheng et al. and Vedula et al:

- [*Zheng, X., Seo, J.H., Vedula, V., Abraham, T. and Mittal, R., 2012. "Computational modeling and analysis of intracardiac flows in simple models of the left ventricle." Eur. J. Mech. B Fluids, 35, pp.31-39.*](https://doi.org/10.1016/j.euromechflu.2012.03.002)

- [*Vedula, V., Fortini, S., Seo, J.H., Querzoli, G. and Mittal, R., 2014. "Computational modeling and validation of intraventricular flow in a simple model of the left ventricle." Theor. Comput. Fluid Dyn., 28, pp.589-604.*](https://doi.org/10.1007/s00162-014-0335-4)

Further details about the diagnosis and prognosis applications could be found in the following references:

- [*Bell-Navas, A., Villalba-Orero, M., Lara-Pezzi, E., Garicano-Mena, J., & Clainche, S. L., Heart Failure Prediction using Modal Decomposition and Masked Autoencoders for Scarce Echocardiography Databases. arXiv preprint arXiv:2504.07606, 2025.*](https://arxiv.org/abs/2504.07606)

- [*Bell-Navas, A., Garicano-Mena, J., Ausiello, A., Clainche, S. L., Villalba-Orero, M., & Lara-Pezzi, E., CardioMOD-Net: A Modal Decomposition-Neural Network Framework for Diagnosis and Prognosis of HFpEF from Echocardiography Cine Loops. arXiv preprint arXiv:2601.01176, 2026.*](https://arxiv.org/abs/2601.01176)


# Contributors <a id="contributors"></a>

- Andrés Bell-Navas
- Zhuoqun Zhao
- Ander Sánchez Muñoz
- Eneko Lazpita Suinaga

