---
layout: page
title: "Cardiac Pathology"
area: "Cardiovascular Modelling and Diagnosis"
tldr: "Patient-specific CFD, medical data analysis, reduced-order modelling and AI-based pathology identification."
---

# Overview

This section concerns methods addressing several tasks related with the study of cardiovascular diseases (CVDs): pattern identification, diagnosis and prognosis Modal decomposition and deep learning architectures are used, and also cardiac flow simulations are generated. For this purpose, medical data and CFD databases are used.

# TODO: poner índice de esta página aquí

# CFD & High-Fidelity Simulations

This section presents the tutorials for the simulations based on Computational Fluid Dynamics (CFD) for modeling the intricate dynamics of intracardiac blood flow.

## Tutorials <a id="cfd-tutorials"></a>

- [*Cardiac tutorials*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/): inside this page showing the tutorials, 'CFD tutorial' concerns to the specific one related with this section.



Computational Fluid Dynamics (CFD) has emerged as a key tool for modeling the intricate dynamics of intracardiac blood flow. This approach not only enhances our fundamental understanding of cardiac function, but also paves the way for innovative treatment strategies.

Content:

* [Required tools and software](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#cfd-required-software)
* [Tutorials](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#cfd-tutorials)
* [Results](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#cfd-results)
* [Videos](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#cfd-videos)

## Required tools and software <a id="cfd-required-software"></a>

* [Matlab](https://es.mathworks.com/products/matlab.html)
* [Spyder](https://www.spyder-ide.org/)
* [Star-CCM+](https://plm.sw.siemens.com/en-US/simcenter/fluids-thermal-simulation/star-ccm/?srsltid=AfmBOoqvQTHcTwcvPnM1Fc9M8LCw2NWBRd50mWwnrLL_ZBjIjw5h8dR0)
* [Ansys Fluent](https://www.ansys.com/products/fluids/ansys-fluent)
* [3D Slicer](https://www.slicer.org/)
* [MeshLab](https://www.meshlab.net/)
* [ParaView](https://www.paraview.org/)
* [CT Scans](https://figshare.com/s/2a5de3a2b89a3fb87932?file=5011837)

## Tutorials <a id="cfd-tutorials"></a>
Explore our step-by-step video tutorials on setting up CFD simulations of the left ventricle. These resources include all necessary files to replicate our results, offering a comprehensive guide for anyone aiming to deepen their understanding or reproduce our findings.

The complete tutorial for the CFD & High Fidelity simulations could be found here inside the [*Cardiac tutorials*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/).

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

## Results <a id="cfd-results"></a>
The ideal models of the left ventricle (LV) for our simulations are taken directly from these references and are shown in the following figure. These models essentially represent an idealization of the ventricular cavity with two tubes attached to simulate inflow and outflow through the mitral and aortic valves, respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/geometry_ideal.png?raw=true)

The computational framework used in this study is designed to solve the Navier-Stokes equations, assuming that blood behaves as an incompressible non-Newtonian fluid. We choose laminar flow conditions that are particularly effective in capturing the vortical features of the diastolic phase of the cardiac cycle. Boundary conditions are a critical aspect; therefore, wall motion, inflow and outflow are set to match the ventricular flow rate curve extracted from references. A grid convergence study was performed to ensure that the simulations were fine-tuned.

The primary objective of this study is to examine the formation and evolution of the vortex ring, a prominent flow feature during the E-wave of diastole. The vortex ring plays a pivotal role in cardiac hemodynamics and has been extensively studied in the literature. The vortex ring emerges from the mitral valve during the E-wave of diastole, with its axis aligned with the mitral valve axis. The initial shape of the vortex ring is that of a donut, although it is asymmetric, with a thinner profile closer to the wall. This indicates a healthy heart. As the vortex ring traverses the ventricle, it gradually tilts due to the reduction in inflow velocity. Interactions between the vortex ring and the ventricular walls result in the formation of secondary vortex tubes. These vortex tubes exhibit complex instabilities, which ultimately result in their interaction with the vortex ring and its subsequent destabilization. The evolution of this flow structure is depicted in Figures X and Y for the geometries used by Zheng et al. and Vedula et al., respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Zheng_vorticity.png?raw=true)
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Vedula_vorticity.png?raw=true)

This analysis highlights the importance of CFD in advancing our understanding of intracardiac flow dynamics and developing improved diagnostic and therapeutic strategies for cardiovascular diseases.

## Resources & Databases

- Files for geometry pre-processing [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/generateSTLFiles.zip).
- Files for CFD with Star-CCM+ [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Tutorial_Star-CCM+.zip).
- Files for CFD with Ansys Fluent [*here*](https://drive.upm.es/s/A8EuWtjSuMAetHc).

## Videos <a id="cfd-videos"></a>

- **Introduction**: Explanation of the project, integrating CFD simulations with Neural Networks:
<iframe width="560" height="315" src="https://www.youtube.com/embed/XHdfQc7LLgA?si=jY4mia541q-MqgtM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- **Step 1**: Geometry pre-processing:
<iframe width="560" height="315" src="https://www.youtube.com/embed/Bzd_ZniGGG0?si=UvRmu9_2Qd7QxDWJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- **Step 2**: Replicating the blood flow simulations inside the left ventricle using STAR-CCM+:
<iframe width="560" height="315" src="https://www.youtube.com/embed/8YjVIamKzhY?si=U5s0zgmYVJ2fAl5a" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

- **Step 3**: Setting up blood flow simulations within the left ventricle using Ansys Fluent, grouping together everything required to successfully replicate the results:
<iframe width="560" height="315" src="https://www.youtube.com/embed/zkAAioOEVDE?si=VAc7JBNCvohALkOS" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# AI & Data-Driven Models

This section presents the tutorials to use the methods combining Artificial Intelligence and Modal Decomposition for pattern identification, diagnosis and prognosis of cardiovascular diseases.

## Tutorials <a id="ai-tutorials"></a>

- [*Cardiac tutorials*](https://modelflows.github.io/modelflowsapp/software/tutorials/cardiac-tutorials/): : inside this page showing the tutorials, 'Diagnosis tutorial' and 'Prognosis tutorial' concern to the specific ones related with this section.

## Notebooks

- [*Diagnosis Notebooks*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/diagnosis_tutorial/notebooks): this link goes to the source files and to the guide of how to use the codes implementing the training and testing of models for the diagnosis of cardiovascular diseases (CVD).
- [*Prognosis Notebooks*](https://github.com/modelflows/ModelFLOWs-cardiac/tree/main/prognosis_tutorial/notebooks): this link goes to the source files and to the guide of how to use the codes implementing the training and testing of models for the prognosis of heart failures.

## Resources & Databases

- Dataset: confidential CNIC datasets.

# Publications

Further details about the diagnosis and prognosis applications could be found in the following references:

- [*Bell-Navas, A., Villalba-Orero, M., Lara-Pezzi, E., Garicano-Mena, J., & Clainche, S. L., Heart Failure Prediction using Modal Decomposition and Masked Autoencoders for Scarce Echocardiography Databases. arXiv preprint arXiv:2504.07606, 2025.*](https://arxiv.org/abs/2504.07606)

- [*Bell-Navas, A., Garicano-Mena, J., Ausiello, A., Clainche, S. L., Villalba-Orero, M., & Lara-Pezzi, E., CardioMOD-Net: A Modal Decomposition-Neural Network Framework for Diagnosis and Prognosis of HFpEF from Echocardiography Cine Loops. arXiv preprint arXiv:2601.01176, 2026.*](https://arxiv.org/abs/2601.01176)

For validation of the CFD simulations, we base our study on the work of Zheng et al. and Vedula et al:

- [*Zheng, X., Seo, J.H., Vedula, V., Abraham, T. and Mittal, R., 2012. "Computational modeling and analysis of intracardiac flows in simple models of the left ventricle." Eur. J. Mech. B Fluids, 35, pp.31-39.*](https://doi.org/10.1016/j.euromechflu.2012.03.002)

- [*Vedula, V., Fortini, S., Seo, J.H., Querzoli, G. and Mittal, R., 2014. "Computational modeling and validation of intraventricular flow in a simple model of the left ventricle." Theor. Comput. Fluid Dyn., 28, pp.589-604.*](https://doi.org/10.1007/s00162-014-0335-4)

# Contributors

- Andrés Bell-Navas
- Zhuoqun Zhao
- Ander Sánchez Muñoz
- Eneko Lazpita Suinaga

