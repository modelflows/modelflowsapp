---
layout: page
title: Combustion
subtitle: Our studies focused on combustion
---

Content:
1.  [Adaptive prediction](https://modelflows.github.io/modelflowsapp/combustion/#adaptive-prediction)
    *  [Tutorials](https://modelflows.github.io/modelflowsapp/combustion/#tutorials)
       *  [Geometry](https://modelflows.github.io/modelflowsapp/combustion/#geometry)
       *  [Meshing](https://modelflows.github.io/modelflowsapp/combustion/#meshing)
       *  [CFD with OpenFOAM](https://modelflows.github.io/modelflowsapp/combustion/#cfd-with-openfoam)
    *  [Results](https://modelflows.github.io/modelflowsapp/combustion/#results)
       *  [LES results](https://modelflows.github.io/modelflowsapp/combustion/#les-results)
       *  [Prediction by hybrid ROM](https://modelflows.github.io/modelflowsapp/combustion/#geometry)
       *  [Coupling of OpenFOAM and adaptive prediction](https://modelflows.github.io/modelflowsapp/combustion/#coupling-of-adaptive)

2.  [LcSVD-DA](https://modelflows.github.io/modelflowsapp/combustion/#lcsvd-da)

3.  [LcHODMD-DA](https://modelflows.github.io/modelflowsapp/combustion/#lchodmd)


## Adaptive prediction
Large Eddy Simulations (LES) have been widely used in various scenarios due to their capability of capturing more detailed flow fields than those captured by Reynolds-Averaged Navier–Stokes (RANS) simulations and consuming fewer computational resources than Direct Numerical Simulations (DNS). However, for applications involving large-scale devices and combustion, huge computational resources are still required. Recent developments in machine learning have introduced innovative methods for accelerating Computational Fluid Dynamics (CFD). Among these, the adaptive method combining CFD and hybrid reduced order models (ROMs) is a promising way to accelerate the simulations [1]. This approach not only enhances our fundamental understanding of combustion patterns but also paves the way for innovative strategies to improve the combustion efficiency.
For validation purposes, we perform LES and adaptive prediction on a typical jet in hot coflow burner used by Dally et al [2]. 

<!-- REFERENCES -->
[*Abadía-Heredia, R., López-Martín, M., Carro, B., Arribas, J. I., Pérez, J. M., & Le Clainche, S. (2022). A predictive hybrid reduced order model based on proper orthogonal decomposition combined with deep learning architectures. Expert Systems with Applications, 187, 115910.*](https://doi.org/10.1016/j.eswa.2021.115910)

[*Dally, B. B., Karpetis, A. N., & Barlow, R. S. (2002). Structure of turbulent non-premixed jet flames in a diluted hot coflow. Proceedings of the combustion institute, 29(1), 1147-1154.*](https://doi.org/10.1016/S1540-7489(02)80145-6)

### Tutorials
Discover our detailed tutorials that walk you through the process of setting up Computational Fluid Dynamics (CFD) simulations.

#### Geometry
The geometry of JHC burner is shown in the following figure. The burner consists of a central jet (I.D. = 4.25 mm) and an annulus (I.D. = 82 mm). As the burner was mounted in a wind tunnel, there was an air flow inlet around the annulus tube.
<!-- IMAGES -->
<!--  ![Geometry of JHC burner](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_geometry.png?raw=true) -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_geometry.png?raw=true" alt="Figure text" width="80%">
</p>

#### Meshing
The mesh can be generated with several tools, such as SnappyHexMesh, BlockMesh, Ansys ICEM CFD, and fluent Meshing etc. The mesh employed is shown in the following figure. The total number of grid cells is 1, 600, 000. 
<!-- IMAGES -->
<!--  ![Mesh of JHC burner](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_mesh.png?raw=true) -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_mesh.png?raw=true" alt="Figure text" width="80%">
</p>

#### CFD with OpenFOAM
This section provides a complete guide on how to set combustion simulations using OpenFOAM-v10. We focus on one case (HM3) in the paper of Dally et al. A mixture of H2 and CH4, equal in volume, was used as the fuel in the central jet. The annulus was fed with O2, N2, H2O and CO2 with mass fractions of 9%, 79%, 6.5% and 5.5%. The mean temperature of fuel jet, hot co - flow, and air inlet is 305, 1300, and 300 K, respectively. The Reynolds number of fuel jet is 9482, and the velocity of both hot co-flow and air inlet is 3.2 m/s.

*Tutorial coming soon...*

### Results
This section presents the simulation results of JHC burner. 

#### LES results
The contours of temperature, mass fractions of CH4, CO2 are shown as follows. 
<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_T_CH4_CO2.png?raw=true)

#### Prediction by hybrid ROM
Based on the data set obtained by CFD simulations, the evolution process of flow field was forecast by hybrid ROM. The temperature distributions of two cut planes are shown as follows. 
<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_prediction_T_plane1.png?raw=true)
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_burner_prediction_T_plane2.png?raw=true)

#### Coupling of OpenFOAM and adaptive prediction
*Work in progress. Coming soon…*



## LcSVD-DA
One of the primary challenge associated with the combustion datasets is their heterogeneous nature. The experimental database is normally generated by assimilating the information extracted from a series of sensors placed in the dynamical system. Unlike the sparsely resolved spatial data obtained through experiments we can generate highly resolved spatial information of combustion systems through large eddy simulations (LES) or direct numerical simulations (DNS).
These two datasets (experimental and theoretical) independently hold significant information about the combustion system.LcSVD data assimilation is a mathematical framework for data assimilation that can simultaneously analyze both datasets by extracting physical information, complementing data, correcting divergent tendencies, and addressing spurious measurements.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/f2cc14f96da7255149471ca3d1aeed99de96c7c1/assets/img/2025_01_30_pillai_lcsvd-da.png?raw=true)

### Results
The results of applying lcsvd-da algorithm to laminar co-flow flame dataset with fuel 65% methane and 35% nitrogen. The figure shows original database (left), reconstructed database using lcSVD data assimilation (center) and downsampled matrix (right) for species Temperature, OH and Methane (top to bottom).

![Figure text](https://github.com/modelflows/modelflowsapp/blob/f2cc14f96da7255149471ca3d1aeed99de96c7c1/assets/img/re1_lcsvd-da_lam.png?raw=true)

The results of applying lcsvd-da algorithm to turbulent bluff body stabilized hydrogen flame dataset. The figure shows original database (left), reconstructed database using lcSVD data assimilation (center) and downsampled matrix (right) for variables stream-wise velocity(top) and normal velocity(bottom).

![Figure text](https://github.com/modelflows/modelflowsapp/blob/f2cc14f96da7255149471ca3d1aeed99de96c7c1/assets/img/re2_lcsvd-da_turb.png?raw=true)


## LcHODMD
Reactive flow databases are typically large, complex, and heterogeneous. Experimental data, on the one hand, is often gathered using a sparse array of sensors. While this sparsity poses limitations, it can still provide critical insights during real-time analysis and decision-making. On the other hand, simulation datasets are characterized by their high dimensionality and intricate information, which makes processing them with standard SVD computationally expensive and time-consuming. As datasets grows size, the scalability of standard SVD becomes a significant bottleneck, particularly in applications requiring repeated computations. Low-Cost Higher Order Dynamic Mode Decomposition (lcHODMD) is a lightweight extension of standard HODMD, designed to reduce memory usage and computational time . This method can be implemented using either Low-Cost Singular Value Decomposition (lcSVD) or Low-Cost Higher Order Singular Value Decomposition (lcHOSVD). 

![Figure text](https://github.com/modelflows/modelflowsapp/blob/621c629e76f9f1dabd7d0199c6158c956184a662/assets/img/2025_01_30_pillai_lchodmd.png?raw=true)

### Results
The results of applying lcHODMD algorithm to laminar co-flow flame dataset with fuel 65% methane and 35% nitrogen. The figure shows original database , downsampled matrix, reconstructed database using lcHODMD data assimilation and absolute error (left to right) for species Temperature, OH and Methane (top to bottom).

![Figure text](https://github.com/modelflows/modelflowsapp/blob/621c629e76f9f1dabd7d0199c6158c956184a662/assets/img/re3_lchodmd_lam.png?raw=true)

The results of applying lcHODMD algorithm to turbulent bluff body stabilized hydrogen flame dataset. The figure shows original database , downsampled matrix, reconstructed database using lcHODMD data assimilation and absolute error (left to right) for variables stream-wise velocity(top) and normal velocity(bottom).

![Figure text](https://github.com/modelflows/modelflowsapp/blob/621c629e76f9f1dabd7d0199c6158c956184a662/assets/img/re3_lchodmd_turb.png?raw=true)
