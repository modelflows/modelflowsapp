---
layout: page
title: ModelFLOWs-cardiac
subtitle: Our studies focused on cardiovascular diseases
---

ModelFLOWs-cardiac, a branch of the ModelFLOWs-app which contains an open source Software for pattern identification, classification and prediction of cardiovascular diseases (CVDs) using modal decomposition and deep learning architectures, together with CFD databases and codes for obtention of cardiac flow simulations. 

 ***Main projects funding this research:***

*2022-2024. DigitHEART (New tools and models based on CFD and non-invasive imaging to predict heart disease progression and response to treatment). Plan de Recuperación, Transformación y Resiliencia–Ministerio de Ciencia e Innovación, Spain, TED2021-129774B-C21.*

*2022-2025. CardioAging (Mecanometabolismos de la insuficiencia cardíaca asociada a la edad). Líneas Estratégicas–Ministerio de Ciencia e Innovación, Spain, PLEC2022-009235.*

Content:

1-  [Medical Data](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection#medical-data)

  *  [Pattern Detection](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection/#pattern-medical)
  *  [Classification](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection/#classification)
  *  [Prediction](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection/#prediction)

2-  [CFD Data](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection/#cfd-data)

  *  [Tutorials](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection/#tutorials)
  *  [Pattern Detection](https://modelflows.github.io/modelflowsapp/cardiacpathologydetection/#pattern-cfd)


This data-driven application consists of two modules: **Medical data** and **CFD data**. The first one contains three blocks: *Pattern detection*, *Classification* and *Prediction*. The latter one contains two blocks: *Codes and simulations* and *Pattern detection*.

## Medical data
The medical imaging datasets used for this first application are echocardiography video loops and magnetic resonance imaging (MRI): 
1.	The echocardiography videos are taken with respect to two views: long axis and shorts axis views (LAX and SAX respectively). The images are taken from mice with different cardiac conditions including healthy, diabetic cardiomyopathy, myocardial infarction, obesity, TAC hypertrophy). Each video consists of ~120 frames (snapshots).
2.	The MRI dataset consists of 10 MRI sequences, representing 10 different slices of the heart.  In particular, 20 images (snapshots) of 128 × 128 × 1 resolution were acquired for each slice, resulting a total number of 200 snapshot per dataset. 

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFloes_Cardiac_IMAGE00.png?raw=true)

### Pattern detection <a id="pattern-medical"></a>
#### HODMD

Medical imaging field is being profoundly affected by the technological revolution brought forward by increasingly sophisticated electronic devices and the continuous growth of computing power. Therefore, medical imaging has become a data intensive field: optimized tools grounded in the data science discipline are necessary to reap the full potential of the wealth of data available.
starting from a certain point, approaches based on matrix decomposition and data-driven methods began to gain recognition in medical analysis field. In this research, we focused on the fluid dynamic tool, the higher order dynamic mode decomposition (HODMD). In the following the HODMD was applied to the analysis of echocardiography images as a feature detection technique, with the aim of identifying main patterns related to different cardiac conditions.


#### Analysis and findings

The main process for the higher order dynamic mode decomposition (HODMD) analysis pipeline is summarized in the schematic diagram. The first step is data preparation: each frame (snapshot) extracted from the video loop is cropped (removing the parts with the medical information), then  arranged in a tensor, which is then used as the HODMD input. In the following steps, HODMD decomposes the data into a set of DMD modes, each associated with its own frequency, growth rate and amplitude.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_IMAGE01.jpg?raw=true)

The analysis of the echocardiography datasets using the HODMD algorithm resulted in two main outcomes: (i) identify and segregate two different signals.
The signals, which are regular and periodic, represent the heart rate and respiratory rate. (ii)  Successfully identifying and extracting sets of DMD modes representing the dominant features and patterns related to the different cardiac conditions. These DMD modes display the shape of the heart in its healthy conditions, as well as its shape when afflicted by different cardiac diseases.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_page-IMAGE02.jpg?raw=true)

These results have already been published in :

[*Groun, N., Villalba-Orero, M., Lara-Pezzi, E., Valero, E., Garicano-Mena, J. and Le Clainche, S., 2022. Higher order dynamic mode decomposition: From fluid dynamics to heart disease analysis. Computers in Biology and Medicine, 144, p.105384.*](https://doi.org/10.1016/j.compbiomed.2022.105384)

You can also see the explanation of this paper in the following video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/AOD1t533sd8?si=DS5swbHta_SDBqbc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### Cardiac disease classification
#### Hybrid ROM combining HODMD and CNNs

In this application the HODMD algorithm is combined with convolutional neural networks (CNNs) to improve the classification accuracy of five different cardiac conditions. 
In order to demonstrate this application, two testcases are performed: first, the model (CNN) is trained using a database consists of the original echocardiography images only (testcase 01). Second, the database with the original images is augmented using the DMD modes obtained from the HODMD analysis.

The following sketch summarizes the main steps of the application carried in this work, which can be sectioned into two stages: 
1.	 Feature extraction stage using the HODMD algorithm (as illustrated in the previous application).
2.	 Disease classification using CNNs.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_IMAGE03.jpg?raw=true)

The results obtained from all testcases, and experiments showed a clear improvement in the performance when augmenting the original images using the DMD modes, as it increased the prediction accuracy by 4% - 22%. These results have proved the efficiency of the proposed hybrid tool, which merges model decomposition tools and machine learning approaches, and its ability to enhance classification models and improve predictions on new unseen data.

This work has been used to produce a journal paper, which has been subbmited and currently under review in the journal of Artificial Intelligence In Medicine.

#### HODMD-based reduced order model for cardiac MRI analysis

In this application, the HODMD algorithm is used as a reduced order model (ROM) to generate new MRI databases covering more cardiac cycles, varying for longer periods of time. In particular, the HODMD algorithm is applied to the MRI database with a change in the temporal term of the HODMD expansion. As a consequence, the new database generated will consist of 100 snapshots for each slice instead of 20 snapshots. In this way, we will be able to represent the heart, with additional reconstructed snapshots covering more than one cardiac cycle. Additionally, applying the HODMD algorithm to the tensor containing all the MRI sequences permits the use of the HODMD extrapolation properties to fill in any gaps between the individual slices. As a consequence, a 3D visualization of the full heart can be carried out.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_IMAGE05.jpg?raw=true)


#### SVD Based interpolation tool for information recovery

This new method is applied to the tensor containing all the reconstructed slices in order to recover the information of one missing slice. In particular, the 7th slice has been completely removed, and the two neighboring slices (slice 06 and slice 08) are used to reconstruct all the information of the missing slice. This approach employs the SVD to provide matrix decomposition, while  Spline interpolation is used to recover the information of the missing MR images by interpolating through the points of the matrix of the right singular vectors.

A comparison between the snapshot of the original 7th and the same snapshot from the new interpolated slice is shown in the following figure. As seen the images present a qualitative similar shapes and intensities. The noise is the main difference found between the two slices; hence the reconstructed images are clean.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFloes_Cardiac_IMAGE06.png?raw=true)


These results have already been published in :

[*Groun, N., Villalba-Orero, M., Lara-Pezzi, E., Valero, E., Garicano-Mena, J. and Le Clainche, S., 2022. A novel data-driven method for the analysis and reconstruction of cardiac cine MRI. Computers in Biology and Medicine, 151, p.106317.*](https://doi.org/10.1016/j.compbiomed.2022.106317)

You can also see the explanation of this paper in the following video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/3oJoGSxvK40?si=5ZZyUISubRJENcbQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


#### Vision Transformers
<!-- Andres's work -->
This framework implements an automatic cardiac pathology recognition system which analyses in real-time echocardiography video sequences. This works in two stages. The first one creates a large collection of annotated images from different sources of echocardiography videos. This allows to train any machine learning-based frameworks, especially deep learning-based ones. This stage involves the use of modal decomposition techniques, namely, the Singular Value Decomposition (SVD) and the HODMD algorithms, for the first time to the authors’ knowledge, for both data augmentation and feature extraction in the medical field, in a similar way as explained in the Pattern Detection block. The second stage is aimed to build and train a Vision Transformer (ViT), barely explored in the related literature about heart disease recognition in echocardiography images using deep learning. The ViT is adapted for an effective training from scratch, even with scarce databases, usual in the medical field. This designed neural network analyses the images from an echocardiography video to predict the heart state. In this section, the diagnosis or classification task is covered, that is, the classification between different cardiac conditions. 

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01Jan_30_Bell_DiagnosisOverview.jpg?raw=true)


The results obtained show the efficacy of the HODMD algorithm and the superiority of the proposed system, even outperforming pretrained Convolutional Neural Networks (CNNs), the method of choice in the literature. 

Further details about the work explained in this section could be found in the following reference:

[*Bell-Navas, A., Groun, N., Villalba-Orero, M., Lara-Pezzi, E., Garicano-Mena, J., & Le Clainche, S., 2025. “Automatic Cardiac Pathology Recognition in Echocardiography Images using Higher Order Dynamic Mode Decomposition and a Vision Transformer for Small Datasets.” Exp. Syst. Appl., 264, 125849.*](https://doi.org/10.1016/j.eswa.2024.125849)

<!-- The following video summarizes the developed system and shows the obtained results in the diagnosis task: -->

The code of the training and testing stages (as python files and notebooks) of the described system, including the requirements file, can be downloaded with the following [*link*](https://github.com/modelflows/ModelFLOWSs-cardiac/raw/refs/heads/main/medical-data/Diagnosis_scripts.zip).

A file with the pretrained weights of the ViT, to skip the training part and directly run the testing stage, can be downloaded with the following [*link*](https://drive.google.com/file/d/1tO9dv1zjzObGCOOrsoJgYpPxQZYdi2BC/view?usp=drive_link). 

### Prediction
#### Vision Transformers
<!-- Andres's work -->

This section considers the application of the system described above for the prognosis task, which is a challenging regression task consisting in predicting the time in which a heart failure will happen. In a similar way, the system first creates a large database of annotated images from different sources of echocardiography videos. For this purpose, the use of the SVD and the HODMD algorithms for both feature extraction and data augmentation is involved. After this machine learning-compatible database creation, a ViT is built and trained with Self-supervised learning (SSL) methods to deal with scarce databases of echocardiograms. This designed ViT analyses images from an echocardiography video sequence to predict the time in which a heart failure will happen.  

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01Jan_30_Bell_PrognosisOverview.jpg?raw=true)

This work has been used to produce a journal article, which is currently in the process of elaboration. 

<!-- The following video summarizes the developed system with the obtained results in the prognosis task:  -->

*Code in progress. Coming soon...*


## CFD Data
The growing impact of cardiovascular disease (CVD) requires advances in diagnosis and treatment. Recent developments in medical research have introduced innovative methods for understanding and treating complex diseases such as CVDs. Among these, Computational Fluid Dynamics (CFD) has emerged as a key tool for modeling the intricate dynamics of intracardiac blood flow. This approach not only enhances our fundamental understanding of cardiac function, but also paves the way for innovative treatment strategies.

For validation purposes, we base our study on the work of Zheng et al. and Vedula et al:

[*Zheng, X., Seo, J.H., Vedula, V., Abraham, T. and Mittal, R., 2012. "Computational modeling and analysis of intracardiac flows in simple models of the left ventricle." Eur. J. Mech. B Fluids, 35, pp.31-39.*](https://doi.org/10.1016/j.euromechflu.2012.03.002)

[*Vedula, V., Fortini, S., Seo, J.H., Querzoli, G. and Mittal, R., 2014. "Computational modeling and validation of intraventricular flow in a simple model of the left ventricle." Theor. Comput. Fluid Dyn., 28, pp.589-604.*](https://doi.org/10.1007/s00162-014-0335-4)

You can also see the explanation of this project in the following video:
<iframe width="560" height="315" src="https://www.youtube.com/embed/XHdfQc7LLgA?si=jY4mia541q-MqgtM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


### Tutorials
Explore our step-by-step video tutorials on setting up CFD simulations of the left ventricle. These resources include all necessary files to replicate our results, offering a comprehensive guide for anyone aiming to deepen their understanding or reproduce our findings. 

#### Geometry Pre-Processing
This section provides our MATLAB codes for generating STL file sequences that define ventricular wall motion for CFD simulations. The workflow is based on integrating ventricular volume variation from a flow rate chart that describes the quantity of blood coming in and out of the left ventricle.

We offer two approaches:
* Idealized Geometry: Where the wall motion is defined analytically, and STL files are generated accordingly. 
* Patient-Specific Geometry: Requires code adjustments since analytical expressions are unavailable. This process includes extracting the left ventricle model from cardiotomography data to ensure accurate patient-specific simulations.

Download the necessary files [*here*](https://github.com/modelflows/ModelFLOWSs-cardiac/raw/refs/heads/main/CFD/generateSTLFiles.zip).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWSs-cardiac/raw/refs/heads/main/CFD/Slides_Tutorial_GeometryPreprocessing.pptx).

<iframe width="560" height="315" src="https://www.youtube.com/embed/Bzd_ZniGGG0?si=UvRmu9_2Qd7QxDWJ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

#### CFD with Star-CCM+
This section provides a complete guide on replicating our blood flow simulations inside the left ventricle using STAR-CCM+. From loading the geometry and meshing to configuring the simulation settings, we walk you through each step to ensure accurate reproduction of our results.

Download the necessary files [*here*](https://github.com/modelflows/ModelFLOWSs-cardiac/raw/refs/heads/main/CFD/Tutorial_Star-CCM+.zip).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWSs-cardiac/raw/refs/heads/main/CFD/Slides_Tutorial_StarccmCFD.pptx).

<iframe width="560" height="315" src="https://www.youtube.com/embed/8YjVIamKzhY?si=U5s0zgmYVJ2fAl5a" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

#### CFD with Ansys Fluent
In this section, we outline the entire process of setting up blood flow simulations within the left ventricle using Ansys Fluent. From importing the geometry and generating the mesh to configuring the simulation parameters, this guide covers everything needed to successfully replicate our results.

Download the necessary files [*here*](https://drive.upm.es/s/A8EuWtjSuMAetHc).

Download the slides [*here*](https://github.com/modelflows/ModelFLOWSs-cardiac/raw/refs/heads/main/CFD/Slides_Tutorial_FluentCFD.pptx).

<iframe width="560" height="315" src="https://www.youtube.com/embed/zkAAioOEVDE?si=VAc7JBNCvohALkOS" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

You can obtain the necessary tools and softwares here:
* [Matlab](https://es.mathworks.com/products/matlab.html)
* [Spyder](https://www.spyder-ide.org/)
* [Star-CCM+](https://plm.sw.siemens.com/en-US/simcenter/fluids-thermal-simulation/star-ccm/?srsltid=AfmBOoqvQTHcTwcvPnM1Fc9M8LCw2NWBRd50mWwnrLL_ZBjIjw5h8dR0)
* [Ansys Fluent](https://www.ansys.com/products/fluids/ansys-fluent)
* [3D Slicer](https://www.slicer.org/)
* [MeshLab](https://www.meshlab.net/)
* [ParaView](https://www.paraview.org/)
* [CT Scans](https://figshare.com/s/2a5de3a2b89a3fb87932?file=5011837)

### Results
The ideal models of the left ventricle (LV) for our simulations are taken directly from these references and are shown in the following figure. These models essentially represent an idealization of the ventricular cavity with two tubes attached to simulate inflow and outflow through the mitral and aortic valves, respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/geometry_ideal.png?raw=true)

The computational framework used in this study is designed to solve the Navier-Stokes equations, assuming that blood behaves as an incompressible non-Newtonian fluid. We choose laminar flow conditions that are particularly effective in capturing the vortical features of the diastolic phase of the cardiac cycle. Boundary conditions are a critical aspect; therefore, wall motion, inflow and outflow are set to match the ventricular flow rate curve extracted from references. A grid convergence study was performed to ensure that the simulations were fine-tuned.

The primary objective of this study is to examine the formation and evolution of the vortex ring, a prominent flow feature during the E-wave of diastole. The vortex ring plays a pivotal role in cardiac hemodynamics and has been extensively studied in the literature. The vortex ring emerges from the mitral valve during the E-wave of diastole, with its axis aligned with the mitral valve axis. The initial shape of the vortex ring is that of a donut, although it is asymmetric, with a thinner profile closer to the wall. This indicates a healthy heart. As the vortex ring traverses the ventricle, it gradually tilts due to the reduction in inflow velocity. Interactions between the vortex ring and the ventricular walls result in the formation of secondary vortex tubes. These vortex tubes exhibit complex instabilities, which ultimately result in their interaction with the vortex ring and its subsequent destabilization. The evolution of this flow structure is depicted in Figures X and Y for the geometries used by Zheng et al. and Vedula et al., respectively.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Zheng_vorticity.png?raw=true)
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Vedula_vorticity.png?raw=true)

This analysis highlights the importance of CFD in advancing our understanding of intracardiac flow dynamics and developing improved diagnostic and therapeutic strategies for cardiovascular diseases.


### Pattern detection <a id="pattern-cfd"></a>
*Work in progress. Coming soon...*
<!-- Introduce here the work in progress for pattern detection in CFD cardiac flows with SVD, HODMD, etc. -->
