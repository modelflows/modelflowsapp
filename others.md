---
layout: page
title: Other Useful Codes 
subtitle: 
---

<!-- Comment -->

## Data Assiilation 
Accurate predictions in **Computational Fluid Dynamics (CFD)** rely on precise modeling of fluid behavior, yet uncertainties in simulations often limit their reliability. **Data Assimilation (DA)** helps bridge this gap by combining experimental data with numerical models to refine predictions. However, DA can be computationally expensive, particularly for large-scale applications where **high-resolution (HR)** simulations demand significant resources.
Our research introduces a novel **Reduced-Order Model (ROM)** that merges experimental data and numerical simulations using **DA** to enhance **CFD** predictions. By implementing the **Ensemble Kalman Filter (EnKF)** within a **reduced-dimension framework**, we enable accurate state estimation from limited observations while significantly reducing computational costs. Our method applies **low-resolution (LR)** techniques, including **dataset downsampling** and advanced **reconstruction** methods like **low-cost Singular Value Decomposition (lcSVD)** and **Multi-Dimensional Interpolation (MDI)**, to efficiently restore high-resolution details. The **lcSVD** approach, never before applied to **DA**, provides an innovative way to improve accuracy with minimal computational overhead. This strategy demonstrates that the framework is both **accurate** and **computationally efficient**, making it suitable for **real-time** and **large-scale** fluid dynamics applications. The method will be integrated into the next version of **ModelFLOWs-app**, enhancing its capabilities for industrial and environmental simulations.

More details about the implementation, the reconstruction methods, and EnKF can be found respectively in:

<!-- REFERENCES -->
[Jeanney, P., Hetherington, A., Ahmed, S. E., Lanceta, D., Saiz, S., Perez, J. M. \& Le Clainche, S. (2024). Ensemble Kalman Filter for Data Assimilation coupled with low-resolution computations techniques applied in Fluid Dynamics, to appear on arXiv, 2025.]()

[Hetherington, A., & Clainche, S. L. (2023). Low-cost singular value decomposition with optimal sensor placement. arXiv preprint arXiv:2311.09791.](https://arxiv.org/abs/2311.09791)

[Ahmed, S. E., Pawar, S., & San, O. (2020). PyDA: A hands-on introduction to dynamical data assimilation with python. Fluids, 5(4), 225.](https://www.mdpi.com/2311-5521/5/4/225)

<!-- LINKS -->
[WORD](LINK)
[TO LINK TO SPECIFIC PLACE IN PAGE](https://modelflows.github.io/modelflowsapp/THEPAGE/#THESECTIONNAME)
You can also add <a id="pattern-medical"></a> beside the section to override the label

<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true)

<!-- VIDEOS -->
<iframe width="560" height="315" src="LINK-EXTRACTED-FROM-YOUTUBE-CODE" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<video width="640" height="360" controls><source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/YOURVIDEOHERE.mp4?raw=true" type="video/mp4">
