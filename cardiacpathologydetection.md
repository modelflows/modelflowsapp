---
layout: page
title: ModelFLOWs-cardiac
subtitle: Our studies focused on cardiovascular diseases
---

ModelFLOWs-cardiac, a branch of the ModelFLOWs-app which contains an open source Software for pattern identification, classification and prediction of cardiovascular diseases (CVDs) using modal decomposition and deep learning architectures, together with CFD databases and codes for obtention of cardiac flow simulations. 

This data-driven application consists of two modules: **Medical data** and **CFD data**. The first one contains three blocks: *Pattern detection*, *Classification* and *Prediction*. The latter one contains two blocks: *Codes and simulations* and *Pattern detection*

## Medical data
The medical imaging datasets used for this first application are echocardiography video loops and magnetic resonance imaging (MRI): 
1.	The echocardiography videos are taken with respect to two views: long axis and shorts axis views (LAX and SAX respectively). The images are taken from mice with different cardiac conditions including healthy, diabetic cardiomyopathy, myocardial infarction, obesity, TAC hypertrophy). Each video consists of ~120 frames (snapshots).
2.	The MRI dataset consists of 10 MRI sequences, representing 10 different slices of the heart.  In particular, 20 images (snapshots) of 128 × 128 × 1 resolution were acquired for each slice, resulting a total number of 200 snapshot per dataset. 

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFloes_Cardiac_IMAGE00.png?raw=true)

### Pattern detection
#### HODMD
<!-- Nourel's work -->

Medical imaging field is being profoundly affected by the technological revolution brought forward by increasingly sophisticated electronic devices and the continuous growth of computing power. Therefore, medical imaging has become a data intensive field: optimized tools grounded in the data science discipline are necessary to reap the full potential of the wealth of data available.
starting from a certain point, approaches based on matrix decomposition and data-driven methods began to gain recognition in medical analysis field. In this research, we focused on the fluid dynamic tool, the higher order dynamic mode decomposition (HODMD). In the following the HODMD was applied to the analysis of echocardiography images as a feature detection technique, with the aim of identifying main patterns related to different cardiac conditions.

<!-- [*Le Clainche & Vega, Higher order dynamic mode decomposition, SIAM J. Appl. Dyn. Syst., 16(2), 882-925, 2017.*](https://epubs.siam.org/doi/10.1137/15M1054924) -->

#### Analysis and findings

The main process for the higher order dynamic mode decomposition (HODMD) analysis pipeline is summarized in the schematic diagram. The first step is data preparation: each frame (snapshot) extracted from the video loop is cropped (removing the parts with the medical information), then  arranged in a tensor, which is then used as the HODMD input. In the following steps, HODMD decomposes the reshaped data into a set of DMD modes, each associated with its own frequency, growth rate and amplitude.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_IMAGE01.jpg?raw=true)

The analysis of the echocardiography datasets using the HODMD algorithm resulted in two main outcomes: (i) identify and segregate two different signals.
The signals, which are regular and periodic, represent the heart rate and respiratory rate. (ii)  Successfully identifying and extracting sets of DMD modes representing the dominant features and patterns related to the different cardiac conditions. These DMD modes display the shape of the heart in its healthy conditions, as well as its shape when afflicted by different cardiac diseases.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_page-IMAGE02.jpg?raw=true)

These results have already been published in :

[*Groun, N., Villalba-Orero, M., Lara-Pezzi, E., Valero, E., Garicano-Mena, J. and Le Clainche, S., 2022. Higher order dynamic mode decomposition: From fluid dynamics to heart disease analysis. Computers in Biology and Medicine, 144, p.105384.*](https://doi.org/10.1016/j.compbiomed.2022.105384)

You can also see the explanation of this paper in the following video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/watch?v=AOD1t533sd8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<!-- FOR VIDEOS UPLOADED ON GITHUB (upload them on assets/vid/ )
<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/HODMD-video.mp4?raw=true" type="video/mp4">
</video>  -->

<!-- FOR VIDEOS IN YOUTUBE: <iframe width="560" height="315" src="https://www.youtube.com/embed/ZKeShcM8nuI?si=jOUu3mio-dZYFxf5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe> -->

### Classification
#### HODMD + NN
<!-- Nourel's work -->
*Work in progress. Coming soon...*

#### Vision Transformers
<!-- Andres's work -->
*Work in progress. Coming soon...*

### Prediction
#### Vision Transformers
<!-- Andres's work -->
*Work in progress. Coming soon...*


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

You can also see the explanation of this project in the following video:
<iframe width="560" height="315" src="https://www.youtube.com/embed/XHdfQc7LLgA?si=jY4mia541q-MqgtM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<!-- Link to starccm codes and databases? -->

### Pattern detection
*Work in progress. Coming soon...*
<!-- Introduce here the work in progress for pattern detection in CFD cardiac flows with SVD, HODMD, etc. -->
