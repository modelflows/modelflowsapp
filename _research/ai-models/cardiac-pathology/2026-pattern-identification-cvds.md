---
layout: page
category: "AI & Data-Driven Models"
topic: "Cardiac Pathology Recognition"
thumbnail: "assets/img/ModelFlows_Cardiac_IMAGE01.jpg"
tldr: "Pattern identification, classification and prediction of cardiovascular diseases using modal decomposition and deep learning."
title: ModelFLOWs-cardiac AI
subtitle: Our studies based on AI focused on cardiovascular diseases
---

ModelFLOWs-cardiac, a branch of the ModelFLOWs-app which contains an open source Software for pattern identification, classification and prediction of cardiovascular diseases (CVDs) using modal decomposition and deep learning architectures, together with CFD databases and codes for obtention of cardiac flow simulations. 

 ***Main projects funding this research:***

*2022-2024. DigitHEART (New tools and models based on CFD and non-invasive imaging to predict heart disease progression and response to treatment). Plan de Recuperación, Transformación y Resiliencia–Ministerio de Ciencia e Innovación, Spain, TED2021-129774B-C21.*

*2022-2025. CardioAging (Mecanometabolismos de la insuficiencia cardíaca asociada a la edad). Líneas Estratégicas–Ministerio de Ciencia e Innovación, Spain, PLEC2022-009235.*

 ***News related to the projects:***
 
[Un doctorando de la ETSIAE investiga en EEUU en simulación de fluidos para mejorar la salud cardiovascular](https://www.upm.es/?id=CON10424&prefmt=articulo&fmt=detail)
 
[Desarrollan un sistema para reconocer patologías cardíacas basado en IA](https://www.upm.es/UPM/SalaPrensa/Noticias_de_investigacion?fmt=detail&prefmt=articulo&id=CON18701)

[Tres proyectos liderados por investigadores de la ETSIAE, elegidos como las mejores tecnologías del programa UPM2T 2025](https://www.upm.es/investigacion?id=CON28327&prefmt=articulo&fmt=detail)

Content:

1-  [Medical Data](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#medical-data)

  *  [Pattern Detection](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#pattern-medical)
  *  [Classification](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#classification)
  *  [Prediction](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#prediction)
  *  [Diagnosis and Prognosis](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#diagnosis-and-prognosis)

2-  [CFD Data](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#cfd-data)

  *  [Pattern Detection](https://modelflows.github.io/modelflowsapp/research/2026-pattern-identification-cvds/#pattern-cfd)


This data-driven application consists of two modules: **Medical data** and **CFD data**. The first one contains three blocks: *Pattern detection*, *Classification* and *Prediction*. The latter one contains one block: *Pattern detection*.

The tutorials devoted to the methods based on Artificial Intelligence (AI) for the diagnosis and prognosis of cardiovascular diseases could be found [*here*](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#ai-tutorials).

## Medical data <a id="medical-data"></a>
The medical imaging datasets used for this first application are echocardiography video loops and magnetic resonance imaging (MRI): 
1.	The echocardiography videos are taken with respect to two views: long axis and shorts axis views (LAX and SAX respectively). The images are taken from mice with different cardiac conditions including healthy, diabetic cardiomyopathy, myocardial infarction, obesity, TAC hypertrophy. Each video consists of ~120 frames (snapshots).
2.	The MRI dataset consists of 10 MRI sequences, representing 10 different slices of the heart. In particular, 20 images (snapshots) of 128 × 128 × 1 resolution were acquired for each slice, resulting a total number of 200 snapshot per dataset. 

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

These results have already been published in:

[*Groun, N., Villalba-Orero, M., Lara-Pezzi, E., Valero, E., Garicano-Mena, J. and Le Clainche, S., 2022. Higher order dynamic mode decomposition: From fluid dynamics to heart disease analysis. Computers in Biology and Medicine, 144, p.105384.*](https://doi.org/10.1016/j.compbiomed.2022.105384)

You can also see the explanation of this paper in the following video:

<iframe width="560" height="315" src="https://www.youtube.com/embed/AOD1t533sd8?si=DS5swbHta_SDBqbc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

### Cardiac disease classification <a id="classification"></a>
#### Hybrid ROM combining HODMD and CNNs

In this application the HODMD algorithm is combined with convolutional neural networks (CNNs) to improve the classification accuracy of five different cardiac conditions. 
In order to demonstrate this application, two testcases are performed: first, the model (CNN) is trained using a database consists of the original echocardiography images only (testcase 01). Second, the database with the original images is augmented using the DMD modes obtained from the HODMD analysis.

The following sketch summarizes the main steps of the application carried in this work, which can be sectioned into two stages: 
1.	 Feature extraction stage using the HODMD algorithm (as illustrated in the previous application).
2.	 Disease classification using CNNs.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_IMAGE03.jpg?raw=true)

The results obtained from all testcases, and experiments showed a clear improvement in the performance when augmenting the original images using the DMD modes, as it increased the prediction accuracy by 4% - 22%. These results have proved the efficiency of the proposed hybrid tool, which merges model decomposition tools and machine learning approaches, and its ability to enhance classification models and improve predictions on new unseen data.

These results have already been published in:

[*Groun, N., Villalba-Orero, M., Casado-Martín, L., Lara-Pezzi, E., Valero, E., Garicano-Mena, J. and Le Clainche, S., 2025. A novel data augmentation tool for enhancing machine learning classification: A new application of the higher order dynamic mode decomposition for improved cardiac disease identification. Results in Engineering, 25, p.104143.*](https://doi.org/10.1016/j.rineng.2025.104143)

#### HODMD-based reduced order model for cardiac MRI analysis

In this application, the HODMD algorithm is used as a reduced order model (ROM) to generate new MRI databases covering more cardiac cycles, varying for longer periods of time. In particular, the HODMD algorithm is applied to the MRI database with a change in the temporal term of the HODMD expansion. As a consequence, the new database generated will consist of 100 snapshots for each slice instead of 20 snapshots. In this way, we will be able to represent the heart, with additional reconstructed snapshots covering more than one cardiac cycle. Additionally, applying the HODMD algorithm to the tensor containing all the MRI sequences permits the use of the HODMD extrapolation properties to fill in any gaps between the individual slices. As a consequence, a 3D visualization of the full heart can be carried out.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFlows_Cardiac_IMAGE05.jpg?raw=true)


#### SVD Based interpolation tool for information recovery

This new method is applied to the tensor containing all the reconstructed slices in order to recover the information of one missing slice. In particular, the 7th slice has been completely removed, and the two neighboring slices (slice 06 and slice 08) are used to reconstruct all the information of the missing slice. This approach employs the SVD to provide matrix decomposition, while  Spline interpolation is used to recover the information of the missing MR images by interpolating through the points of the matrix of the right singular vectors.

A comparison between the snapshot of the original 7th and the same snapshot from the new interpolated slice is shown in the following figure. As seen the images present a qualitative similar shapes and intensities. The noise is the main difference found between the two slices; hence the reconstructed images are clean.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/ModelFloes_Cardiac_IMAGE06.png?raw=true)


These results have already been published in:

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

**Important Note:** this diagnosis framework is different to the diagnosis introduced in our tutorial [*here*](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#ai-tutorials). 

The code in Python version for **Diagnosis** presented in this section could be found [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/legacy-medical-data-tutorials/Diagnosis_scripts.zip). 

The pretrained weights can be downloaded [*here*](https://drive.google.com/file/d/1tO9dv1zjzObGCOOrsoJgYpPxQZYdi2BC/view?usp=drive_link). 

### Prediction <a id="prediction"></a>
#### Masked Autoencoders
<!-- Andres's work -->

This section considers the application of the system described above for the prognosis task, which is a challenging and more specific regression task, not previously addressed in the related literature, to the best of the authors' knowledge, consisting in predicting the time in which a heart failure will happen. In a similar way, the system first creates a large database of annotated images from different sources of echocardiography videos. For this purpose, the use of the SVD and the HODMD algorithms for both feature extraction and data augmentation is involved. After this machine learning-compatible database creation, a ViT is built and trained based on the Masked Autoencoder scheme, in which the pretraining and finetuning stages are performed at the same time, i.e., combining Self-supervised learning (SSL) methods and the Supervised Learning, to deal with scarce databases of echocardiograms. This designed ViT analyses images from an echocardiography video sequence to predict the time in which a heart failure will happen.  

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01Jan_30_Bell_PrognosisOverview.jpg?raw=true)

The experiments performed demonstrate the efficacy of the modal decomposition algorithms for data augmentation and feature extraction, and also the superiority of the proposed system, obtaining more accurate heart failure times than those with Convolutional Neural Networks (CNN) and Vision Transformers (ViT).

Further details about the work explained in this section could be found in the following reference:

[*Bell-Navas, A., Villalba-Orero, M., Lara-Pezzi, E., Garicano-Mena, J., & Clainche, S. L., Heart Failure Prediction using Modal Decomposition and Masked Autoencoders for Scarce Echocardiography Databases. arXiv preprint arXiv:2504.07606, 2025.*](https://arxiv.org/abs/2504.07606)

<!-- The following video summarizes the developed system with the obtained results in the prognosis task:  -->

We encourage readers to follow our step-by-step tutorial introduced [*here*](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#ai-tutorials). 

Download the code for **Prognosis** in Python version [*here*](https://github.com/modelflows/ModelFLOWs-cardiac/raw/refs/heads/main/legacy-medical-data-tutorials/Prognosis_scripts.zip).

The pretrained weights can be downloaded [*here*](https://drive.google.com/file/d/1tyi5j6bJfCB1OhXh6c36eDPT4D8E8dST/view?usp=drive_link). 

A fine-tuned version can be found at Hugging Face [*here*](https://huggingface.co/abellnav/heart-failure-prognosis-echo). 

### Diagnosis and prognosis <a id="diagnosis-and-prognosis"></a>
#### Masked Autoencoders

CardioMOD-Net, an AI-based tool capable of addressing the two challenging aforementioned tasks, diagnosis and prognosis, is presented in this section. Specifically, CardioMOD-Net can recognize different heart states and estimate the precise time in which a heart failure will happen, becoming the first unified frmework which jointly addresses the challenges derived from each task. For this purpose, CardioMOD-Net combines Modal Decomposition techniques and state-of-the-art Deep Learning algorithms adapted to databases of video sequences of echocardiography images. In particular, the SVD and the HODMD algorithms are employed to each video sequence of echocardiography images for feature extraction and data augmentation, obtaining reconstructions and modes. After that, the AI-based tool based on Masked Autoencoders (MAE) is trained using all those data and combining Self-supervised learning (SSL) methods and Supervised Learning, to deal with scarce databases of echocardiograms. Finally, unseen video sequences of echocardiography images are preprocessed and analyzed with the Modal Decomposition techniques and the trained AI-based tool to perform diagnosis and prognosis.

The results obtained show the potential of this unified framework to integrate diagnosis and prognosis in a single architecture. This offers more information about the heart state evolution of a patient, more effectively preventing from heart failures and improving customized medicine.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_12Dec_Belletal_ToolOverview.png?raw=true)

The figure depicts an overview of the developed tool for heart disease recognition, capable of addressing two challenging tasks: diagnosis, as heart state classification, and prognosis, as the estimation of the time of a heart failure. (a) The training process of the developed tool, involving a database of echocardiography videos represented as DICOM files with annotations of the heart states and heart failure times. Before training, data augmentation and feature extraction are applied in four steps: (1) Video sequence preprocessing, (2) Singular Value Decomposition (SVD), (3) Higher Order Dynamic Mode Decomposition (HODMD) applied on the reconstructions obtained with the SVD, and (4) SVD applied on the obtained HODMD modes.
(b) Diagnosis and prognosis performed using the tool, based on Artificial Intelligence (AI), after being trained, on new video sequences of echocardiography images. Similarly, preprocessing and modal decomposition techniques are applied before the inference.

Further details about the work explained in this section could be found in the following reference:

[*Bell-Navas, A., Garicano-Mena, J., Ausiello, A., Clainche, S. L., Villalba-Orero, M., & Lara-Pezzi, E., CardioMOD-Net: A Modal Decomposition-Neural Network Framework for Diagnosis and Prognosis of HFpEF from Echocardiography Cine Loops. arXiv preprint arXiv:2601.01176, 2026.*](https://arxiv.org/abs/2601.01176)

Readers are invited to explore in more detail the [*tutorial*](https://modelflows.github.io/modelflowsapp/software/applications/2026-cardiac-pathology/#ai-tutorials) developed for diagnosis and prognosis, also mentioned at the beginning of this page.

## CFD Data <a id="cfd-data"></a>
The growing impact of cardiovascular disease (CVD) requires advances in diagnosis and treatment. Recent developments in medical research have introduced innovative methods for understanding and treating complex diseases such as CVDs. Among these, Computational Fluid Dynamics (CFD) has emerged as a key tool for modeling the intricate dynamics of intracardiac blood flow. This approach not only enhances our fundamental understanding of cardiac function, but also paves the way for innovative treatment strategies.

For validation purposes, we base our study on the work of Zheng et al. and Vedula et al:

[*Zheng, X., Seo, J.H., Vedula, V., Abraham, T. and Mittal, R., 2012. "Computational modeling and analysis of intracardiac flows in simple models of the left ventricle." Eur. J. Mech. B Fluids, 35, pp.31-39.*](https://doi.org/10.1016/j.euromechflu.2012.03.002)

[*Vedula, V., Fortini, S., Seo, J.H., Querzoli, G. and Mittal, R., 2014. "Computational modeling and validation of intraventricular flow in a simple model of the left ventricle." Theor. Comput. Fluid Dyn., 28, pp.589-604.*](https://doi.org/10.1007/s00162-014-0335-4)

### Pattern detection <a id="pattern-cfd"></a>

This section considers the combination of Proper Orthogonal Decomposition (POD) and Autoencoder (AE) architectures for early detection of cardiac deterioration. In this process, representative flow features characterizing different cardiovascular conditions are extracted from left ventricular flow fields obtained from fluid dynamics simulations. These features are contained in nearly orthogonal POD modes produced by the Autoencoders which capture a specified percentage of kinetic energy.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2026_04Apr_Belletat_PODAEsOverview.png?raw=true)

For small encoding dimensions, POD and Variational Autoencoders (VAE) can generate modes accurately representing the physics and flow features and latent variables corresponding to independent spatial
structures and different frequency content. Moreover, VAEs are less sensible to the latent dimension and better preserve orthogonality between modes with respect to other AE architectures.

Overall, AEs have the potential to reproduce POD-like coherent structures and to extract physically meaningful representations of cardiac flow dynamics, useful for several challenging clinical applications and contributing to clinical decision-making.

Further details about the work explained in this section could be found in the following reference:

[*Lazpita, E., Bell-Navas, A., Garicano-Mena, J., Koumoutsakos, P., Clainche, S. L., A Critical Assessment of Pattern Comparisons Between POD and Autoencoders in Intraventricular Flows. arXiv preprint arXiv:2512.19376, 2025.*](https://arxiv.org/abs/2512.19376)

<!-- Introduce here the work in progress for pattern detection in CFD cardiac flows with SVD, HODMD, etc. -->
