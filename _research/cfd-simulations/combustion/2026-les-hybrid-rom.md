---
layout: page
category: "CFD & High-Fidelity Simulations"
topic: "Combustion-LES-ROM"
thumbnail: "assets/img/JHC_burner_geometry.jpg"
tldr: "LES and predictive hybrid ROMs based on POD combined with deep learning architectures for turbulent jet flames."
title: LES-based POD-DL modeling for Turbulent Jet Flames
subtitle: Our studies focused on combustion
---

Content:
* [LES-hybrid ROM](#lesrom)
   * [CFD setup](#setup)
   * [Results](#results)

* [Related Publications](#pubs)

## LES-hybrid ROM <a id="lesrom"></a>
Large Eddy Simulations (LES) have been widely used in various scenarios due to their capability of capturing more detailed flow fields than those captured by Reynolds-Averaged Navier–Stokes (RANS) simulations and consuming fewer computational resources than Direct Numerical Simulations (DNS). However, for applications involving large-scale devices and combustion, huge computational resources are still required. Recent developments in machine learning have introduced innovative methods for accelerating Computational Fluid Dynamics (CFD). Among these, the method combining CFD and hybrid reduced order models (ROMs) is a promising way to accelerate the simulations [1]. This approach not only enhances our fundamental understanding of combustion patterns but also paves the way for innovative strategies to improve the combustion efficiency.
For validation purposes, we perform LES and prediction on a typical jet in hot coflow burner used by Dally et al [2]. 

<!-- REFERENCES -->
[*Abadía-Heredia, R., López-Martín, M., Carro, B., Arribas, J. I., Pérez, J. M., & Le Clainche, S. (2022). A predictive hybrid reduced order model based on proper orthogonal decomposition combined with deep learning architectures. Expert Systems with Applications, 187, 115910.*](https://doi.org/10.1016/j.eswa.2021.115910)

[*Dally, B. B., Karpetis, A. N., & Barlow, R. S. (2002). Structure of turbulent non-premixed jet flames in a diluted hot coflow. Proceedings of the combustion institute, 29(1), 1147-1154.*](https://doi.org/10.1016/S1540-7489(02)80145-6)

### CFD setup <a id="setup"></a>
Discover our detailed tutorials that walk you through the process of setting up Computational Fluid Dynamics (CFD) simulations.

#### Geometry and Mesh
The geometry of JHC burner is shown in the following figure. The burner consists of a central jet (I.D. = 4.25 mm) and an annulus (I.D. = 82 mm). As the burner was mounted in a wind tunnel, there was an air flow inlet around the annulus tube.
The mesh can be generated with several tools, such as SnappyHexMesh, BlockMesh, Ansys ICEM CFD, and fluent Meshing etc. The mesh employed is shown in the following figure. The total number of grid cells is 1, 960, 000. 
<!-- IMAGES -->
<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_Geometry_mesh.png?raw=true" alt="Figure text" width="70%">
</p>


#### Boundary
A mixture of H2 and CH4, equal in volume, was used as the fuel in the central jet. The annulus was fed with O2, N2, H2O and CO2 with mass fractions of 9%, 79%, 6.5% and 5.5%. The mean temperature of fuel jet, hot co-flow, and air inlet is 305, 1300, and 300 K, respectively. The Reynolds number of fuel jet is 9482, and the velocity of both hot co-flow and air inlet is 3.2 m/s.


### Results <a id="results"></a>
This section presents the simulation results of JHC burner. 

#### LES results
The contours of temperature, velocity, vorticity and mass fractions of typical species are shown as follows. 
<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_LES-results.png?raw=true) 


#### Prediction by hybrid ROM
Based on the data set obtained by CFD simulations, the evolution process of flow field was forecast by hybrid ROM. The comparison of temperature and mass fractions of CO, CO2 and H2O between LES and predicted results are given as follows. 
<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_Prediction.png?raw=true)

Additionally, the predicted temperature and H2O mass fraction are compared with LES results along radial direction at different axial positions and time instants, shown as follows. 
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/JHC_Prediction-curves.png?raw=true)

## Related Publications <a id="pubs"></a>
Zou, X., Abadia-Heredia, R., Saavedra, L., Parente, A., Xue, R., & Clainche, S. L. (2025). Generative artificial intelligence and hybrid models to accelerate LES in reactive flows: Application to hydrogen/methane combustion. arXiv preprint arXiv:2507.08426.(https://doi.org/10.48550/arXiv.2507.08426)

Zou, X., Parente, A., & Le Clainche, S. (2026). Divergence detection and flow structure analysis in POD-DL predictions of a hydrogen-methane flame. European Journal of Mechanics-B/Fluids, 204515. (https://doi.org/10.1016/j.euromechflu.2026.204515)
