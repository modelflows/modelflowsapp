---
layout: page
category: "CFD & High-Fidelity Simulations"
topic: "Cardiac Pathology CFD"
thumbnail: "assets/img/Zheng_vorticity.png"
tldr: "Modeling dynamics of intracardiac blood flow with CFD simulations of the left ventricle."
title: ModelFLOWs-cardiac CFD & Simulations
subtitle: Our studies based on CFD high-fidelity simulations focused on cardiovascular diseases
---

ModelFLOWs-cardiac, a branch of the ModelFLOWs-app which contains an Open Source Software for pattern identification, classification and prediction of cardiovascular diseases (CVDs) using modal decomposition and deep learning architectures, together with CFD databases and codes for obtention of cardiac flow simulations. 

 ***Main projects funding this research:***

*2022-2024. DigitHEART (New tools and models based on CFD and non-invasive imaging to predict heart disease progression and response to treatment). Plan de Recuperación, Transformación y Resiliencia–Ministerio de Ciencia e Innovación, Spain, TED2021-129774B-C21.*

*2022-2025. CardioAging (Mecanometabolismos de la insuficiencia cardíaca asociada a la edad). Líneas Estratégicas–Ministerio de Ciencia e Innovación, Spain, PLEC2022-009235.*

 ***News related to the projects:***
 
[Un doctorando de la ETSIAE investiga en EEUU en simulación de fluidos para mejorar la salud cardiovascular](https://www.upm.es/?id=CON10424&prefmt=articulo&fmt=detail)
 
[Desarrollan un sistema para reconocer patologías cardíacas basado en IA](https://www.upm.es/UPM/SalaPrensa/Noticias_de_investigacion?fmt=detail&prefmt=articulo&id=CON18701)

[Tres proyectos liderados por investigadores de la ETSIAE, elegidos como las mejores tecnologías del programa UPM2T 2025](https://www.upm.es/investigacion?id=CON28327&prefmt=articulo&fmt=detail)

Content:

1-  [CFD Data](https://modelflows.github.io/modelflowsapp/research/2026-cfd-simulations-cvds/#cfd-data)

  *  [Tutorials](https://modelflows.github.io/modelflowsapp/research/2026-cfd-simulations-cvds/#tutorials)
  *  [Results](https://modelflows.github.io/modelflowsapp/research/2026-cfd-simulations-cvds/#results)


The steps to perform high-fidelity CFD simulations of dynamics of blood flow are explained here in this page. The module is **CFD data**, and contains the block *Tutorials*. The detailed explanations with the step-by-step videos and codes are available in these [tutorials](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#cfd).

## CFD Data <a id="cfd-data"></a>
The growing impact of cardiovascular disease (CVD) requires advances in diagnosis and treatment. Recent developments in medical research have introduced innovative methods for understanding and treating complex diseases such as CVDs. Among these, Computational Fluid Dynamics (CFD) has emerged as a key tool for modeling the intricate dynamics of intracardiac blood flow. This approach not only enhances our fundamental understanding of cardiac function, but also paves the way for innovative treatment strategies.

For validation purposes, we base our study on the work of Zheng et al. and Vedula et al:

[*Zheng, X., Seo, J.H., Vedula, V., Abraham, T. and Mittal, R., 2012. "Computational modeling and analysis of intracardiac flows in simple models of the left ventricle." Eur. J. Mech. B Fluids, 35, pp.31-39.*](https://doi.org/10.1016/j.euromechflu.2012.03.002)

[*Vedula, V., Fortini, S., Seo, J.H., Querzoli, G. and Mittal, R., 2014. "Computational modeling and validation of intraventricular flow in a simple model of the left ventricle." Theor. Comput. Fluid Dyn., 28, pp.589-604.*](https://doi.org/10.1007/s00162-014-0335-4)


### Tutorials <a id="tutorials"></a>
The steps performed to set up CFD simulations of the left ventricle are explained here. These resources include all necessary files to replicate our results, offering a comprehensive guide for anyone aiming to deepen their understanding or reproduce our findings. 

#### Geometry Pre-Processing
This section provides our MATLAB codes for generating STL file sequences that define ventricular wall motion for CFD simulations. The workflow is based on integrating ventricular volume variation from a flow rate chart that describes the quantity of blood coming in and out of the left ventricle.

We offer two approaches:
* Idealized Geometry: Where the wall motion is defined analytically, and STL files are generated accordingly. 
* Patient-Specific Geometry: Requires code adjustments since analytical expressions are unavailable. This process includes extracting the left ventricle model from cardiotomography data to ensure accurate patient-specific simulations.

Download the necessary files [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/generateSTLFiles.zip).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Slides_Tutorial_GeometryPreprocessing.pptx).

#### CFD with Star-CCM+
This section provides a complete guide on replicating our blood flow simulations inside the left ventricle using STAR-CCM+. From loading the geometry and meshing to configuring the simulation settings, we walk you through each step to ensure accurate reproduction of our results.

Download the necessary files [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Tutorial_Star-CCM+.zip).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Slides_Tutorial_StarccmCFD.pptx).

#### CFD with Ansys Fluent
In this section, we outline the entire process of setting up blood flow simulations within the left ventricle using Ansys Fluent. From importing the geometry and generating the mesh to configuring the simulation parameters, this guide covers everything needed to successfully replicate our results.

Download the necessary files [*here*](https://drive.upm.es/s/A8EuWtjSuMAetHc).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/CFD_tutorial/Slides_Tutorial_FluentCFD.pptx).

You can obtain the necessary tools and softwares here:
* [Matlab](https://es.mathworks.com/products/matlab.html)
* [Spyder](https://www.spyder-ide.org/)
* [Star-CCM+](https://plm.sw.siemens.com/en-US/simcenter/fluids-thermal-simulation/star-ccm/?srsltid=AfmBOoqvQTHcTwcvPnM1Fc9M8LCw2NWBRd50mWwnrLL_ZBjIjw5h8dR0)
* [Ansys Fluent](https://www.ansys.com/products/fluids/ansys-fluent)
* [3D Slicer](https://www.slicer.org/)
* [MeshLab](https://www.meshlab.net/)
* [ParaView](https://www.paraview.org/)
* [CT Scans](https://figshare.com/s/2a5de3a2b89a3fb87932?file=5011837)

### Results <a id="results"></a>
The ideal models of the left ventricle (LV) for our simulations are taken directly from these references and are shown in the following figure. These models essentially represent an idealization of the ventricular cavity with two tubes attached to simulate inflow and outflow through the mitral and aortic valves, respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/geometry_ideal.png?raw=true)

The computational framework used in this study is designed to solve the Navier-Stokes equations, assuming that blood behaves as an incompressible non-Newtonian fluid. We choose laminar flow conditions that are particularly effective in capturing the vortical features of the diastolic phase of the cardiac cycle. Boundary conditions are a critical aspect; therefore, wall motion, inflow and outflow are set to match the ventricular flow rate curve extracted from references. A grid convergence study was performed to ensure that the simulations were fine-tuned.

The primary objective of this study is to examine the formation and evolution of the vortex ring, a prominent flow feature during the E-wave of diastole. The vortex ring plays a pivotal role in cardiac hemodynamics and has been extensively studied in the literature. The vortex ring emerges from the mitral valve during the E-wave of diastole, with its axis aligned with the mitral valve axis. The initial shape of the vortex ring is that of a donut, although it is asymmetric, with a thinner profile closer to the wall. This indicates a healthy heart. As the vortex ring traverses the ventricle, it gradually tilts due to the reduction in inflow velocity. Interactions between the vortex ring and the ventricular walls result in the formation of secondary vortex tubes. These vortex tubes exhibit complex instabilities, which ultimately result in their interaction with the vortex ring and its subsequent destabilization. The evolution of this flow structure is depicted in Figures X and Y for the geometries used by Zheng et al. and Vedula et al., respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Zheng_vorticity.png?raw=true)
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Vedula_vorticity.png?raw=true)

This analysis highlights the importance of CFD in advancing our understanding of intracardiac flow dynamics and developing improved diagnostic and therapeutic strategies for cardiovascular diseases.