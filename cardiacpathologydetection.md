---
layout: page
title: ModelFLOWs-cardiac
subtitle: Our studies focused on cardiovascular diseases
---

ModelFLOWs-cardiac, a branch of the ModelFLOWs-app which contains an open source Software for pattern identification, classification and prediction of cardiovascular diseases (CVDs) using modal decomposition and deep learning architectures, together with CFD databases and codes for obtention of cardiac flow simulations. 

This data-driven application consists of two modules: **Medical data** and **CFD data**. The first one contains three blocks: *Pattern detection*, *Classification* and *Prediction*. The latter one contains two blocks: *Codes and simulations* and *Pattern detection*

## Medical data
### Pattern detection
#### HODMD
<!-- Nourel's work -->

<!-- [*Le Clainche & Vega, Higher order dynamic mode decomposition, SIAM J. Appl. Dyn. Syst., 16(2), 882-925, 2017.*](https://epubs.siam.org/doi/10.1137/15M1054924) -->

<!-- FOR IMAGES ON GITHUB (upload them on assets/img/ ): ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/modelflowsappscheme.png?raw=true) -->

<!-- FOR VIDEOS UPLOADED ON GITHUB (upload them on assets/vid/ )
<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/HODMD-video.mp4?raw=true" type="video/mp4">
</video>  -->

<!-- FOR VIDEOS IN YOUTUBE
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZKeShcM8nuI?si=jOUu3mio-dZYFxf5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> -->

### Classification
#### HODMD + NN
<!-- Nourel's work -->

#### Vision Transformers
<!-- Andres's work -->

### Prediction
#### Vision Transformers
<!-- Andres's work -->


## CFD data
The growing impact of cardiovascular disease (CVD) requires advances in diagnosis and treatment. Recent developments in medical research have introduced innovative methods for understanding and treating complex diseases such as CVDs. Among these, Computational Fluid Dynamics (CFD) has emerged as a key tool for modeling the intricate dynamics of intracardiac blood flow. This approach not only enhances our fundamental understanding of cardiac function, but also paves the way for innovative treatment strategies.

### Codes and simulations
For validation purposes, we base our study on the work of Zheng et al. and Vedula et al:

[*Zheng, X., Seo, J.H., Vedula, V., Abraham, T. and Mittal, R., 2012. "Computational modeling and analysis of intracardiac flows in simple models of the left ventricle." Eur. J. Mech. B Fluids, 35, pp.31-39.*](https://doi.org/10.1016/j.euromechflu.2012.03.002)

[*Vedula, V., Fortini, S., Seo, J.H., Querzoli, G. and Mittal, R., 2014. "Computational modeling and validation of intraventricular flow in a simple model of the left ventricle." Theor. Comput. Fluid Dyn., 28, pp.589-604.*](https://doi.org/10.1007/s00162-014-0335-4)

Therefore, the ideal models of the left ventricle (LV) for our simulations are taken directly from these references and are shown in the following figure. These models essentially represent an idealization of the ventricular cavity with two tubes attached to simulate inflow and outflow through the mitral and aortic valves, respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/geometry_ideal.png?raw=true)

The computational framework used in this study is designed to solve the Navier-Stokes equations, assuming that blood behaves as an incompressible non-Newtonian fluid. We choose laminar flow conditions that are particularly effective in capturing the vortical features of the diastolic phase of the cardiac cycle. Boundary conditions are a critical aspect; therefore, wall motion, inflow and outflow are set to match the ventricular flow rate curve extracted from references. A grid convergence study was performed to ensure that the simulations were fine-tuned.

The primary objective of this study is to examine the formation and evolution of the vortex ring, a prominent flow feature during the E-wave of diastole. The vortex ring plays a pivotal role in cardiac hemodynamics and has been extensively studied in the literature. The vortex ring emerges from the mitral valve during the E-wave of diastole, with its axis aligned with the mitral valve axis. The initial shape of the vortex ring is that of a donut, although it is asymmetric, with a thinner profile closer to the wall. This indicates a healthy heart. As the vortex ring traverses the ventricle, it gradually tilts due to the reduction in inflow velocity. Interactions between the vortex ring and the ventricular walls result in the formation of secondary vortex tubes. These vortex tubes exhibit complex instabilities, which ultimately result in their interaction with the vortex ring and its subsequent destabilization. The evolution of this flow structure is depicted in Figures X and Y for the geometries used by Zheng et al. and Vedula et al., respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Zheng_vorticity.png?raw=true)
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Vedula_vorticity.png?raw=true)

This analysis highlights the importance of CFD in advancing our understanding of intracardiac flow dynamics and developing improved diagnostic and therapeutic strategies for cardiovascular diseases.

<!-- Link to starccm codes and databases?-->

### Pattern detection
*Work in progress. Coming soon...*
<!-- Introduce here the work in progress for pattern detection in CFD cardiac flows with SVD, HODMD, etc. -->
