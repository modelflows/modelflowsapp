---
layout: page
title: Combustion
subtitle: Our studies focused on combustion
---

Content:

1-  [CFD Data](https://modelflows.github.io/modelflowsapp/combustion/#cfd-data)

  *  [Pattern Detection](https://modelflows.github.io/modelflowsapp/combustion/#pattern-analysis)
  *  [Flow Control](https://modelflows.github.io/modelflowsapp/combustion/#flow-control)
      *  [HOSVD](https://modelflows.github.io/modelflowsapp/combustion/#hosvd)
      *  [HODMD](https://modelflows.github.io/modelflowsapp/combustion/#hodmd-combustion)
  *  [Adaptive prediction](https://modelflows.github.io/modelflowsapp/combustion/#adaptive-prediction)
      *  [Results](https://modelflows.github.io/modelflowsapp/combustion/#results)

Combustion is nice

## CFD Data
Lorem ipsum

### Pattern analysis
Lorem ipsum
<!-- LISTS -->
1.	Adrian
2.	Eneko
3.  Sole
4.  Prajith

### Flow control
*   Re = 79
*   `Re = 55`
*   This
*   Way

#### HOSVD

#### HODMD  <a id="hodmd-combustion"></a>

<!-- REFERENCES -->
[*Corrochano, A., Xavier, D., Schlatter, P., Vinuesa, R. and Le Clainche, S., 2020. Flow structures on a planar food and drug administration (FDA) nozzle at low and intermediate Reynolds number. Fluids, 6(1), p.4.*](https://doi.org/10.3390/fluids6010004)

[Download](https://github.com/modelflows/modelflowsapp/blob/master/assets/datasets/2024_Tagliaferroetal_Databases.zip)

<!-- LINKS -->
[Download matlab]((https://es.mathworks.com/products/matlab.html)
[TO LINK TO SPECIFIC PLACE IN PAGE](https://modelflows.github.io/modelflowsapp/THEPAGE/#THESECTIONNAME)
You can also add <a id="pattern-medical"></a> beside the section to override the label

<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Zheng_vorticity.png?raw=true)

<!-- VIDEOS -->

<iframe width="560" height="315" src="https://www.youtube.com/embed/B5xId8p3EW0?si=rsPdPHjLgpsf3pTY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

<video width="640" height="360" controls><source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/Enhancement_video.mp4?raw=true" type="video/mp4">

### Adaptive prediction
Large Eddy Simulations (LES) have been widely used in various scenarios due to their capability of capturing more detailed flow fields than those captured by Reynolds-Averaged Navier–Stokes (RANS) and consuming fewer computational resources than Direct Numerical Simulations (DNS). However, for applications involving large-scale devices and combustion, huge computational resources are still required. Recent developments in machine learning have introduced innovative methods for accelerating Computational Fluid Dynamics (CFD). Among these, the adaptive method combining CFD and hybrid reduced order models (ROMs) is a promising way to accelerate the simulations. This approach not only enhances our fundamental understanding of combustion patterns but also paves the way for innovative strategies to improve the combustion efficiency.

For validation purposes, we perform LES and adaptive prediction on a typical jet in hot coflow burner used by Dally et al. 
<!-- REFERENCES -->
[*Dally, B. B., Karpetis, A. N., & Barlow, R. S. (2002). Structure of turbulent non-premixed jet flames in a diluted hot coflow. Proceedings of the combustion institute, 29(1), 1147-1154.*](https://doi.org/10.1016/S1540-7489(02)80145-6)

#### Results
The geometry of JHC burner
<!-- IMAGES -->
![Geometry of JHC burner](https://github.com/modelflows/modelflowsapp/assets/img/JHC burner geometry.jpg?raw=true)
