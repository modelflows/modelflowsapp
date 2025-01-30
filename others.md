---
layout: page
title: Other Useful Codes 
subtitle: 
---

<!-- Comment -->

## Data Assimilation 
Accurate predictions in **Computational Fluid Dynamics (CFD)** rely on precise modeling of fluid behavior, yet uncertainties in simulations often limit their reliability. **Data Assimilation (DA)** helps bridge this gap by combining experimental data with numerical models to refine predictions. However, DA can be computationally expensive, particularly for large-scale applications where **high-resolution (HR)** simulations demand significant resources.
Our research introduces a novel **Reduced-Order Model (ROM)** that merges experimental data and numerical simulations using **DA** to enhance **CFD** predictions. By implementing the **Ensemble Kalman Filter (EnKF)** within a **reduced-dimension framework**, we enable accurate state estimation from limited observations while significantly reducing computational costs. Our method applies **low-resolution (LR)** techniques, including **dataset downsampling** and advanced **reconstruction** methods like **low-cost Singular Value Decomposition (lcSVD)** and **Multi-Dimensional Interpolation (MDI)**, to efficiently restore high-resolution details. The **lcSVD** approach, never before applied to **DA**, provides an innovative way to improve accuracy with minimal computational overhead. This strategy demonstrates that the framework is both **accurate** and **computationally efficient**, making it suitable for **real-time** and **large-scale** fluid dynamics applications. The method will be integrated into the next version of **ModelFLOWs-app**, enhancing its capabilities for industrial and environmental simulations.



![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01Jan_30_Jeanney_DA.png?raw=true)

More details about the implementation:

<!-- REFERENCES -->
[Jeanney, P., Hetherington, A., Ahmed, S. E., Lanceta, D., Saiz, S., Perez, J. M. & Le Clainche, S. (2024). Ensemble Kalman Filter for Data Assimilation coupled with low-resolution computations techniques applied in Fluid Dynamics, to be published on arXiv, 2025.]()

<!-- VIDEOS 
<iframe width="560" height="315" src="LINK-EXTRACTED-FROM-YOUTUBE-CODE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<video width="640" height="360" controls><source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/YOURVIDEOHERE.mp4?raw=true" type="video/mp4">
-->
