---
layout: page
title: Modal Decomposition
<!--subtitle: GENERAL SUBTITLE -->
---

Codes available:
1. [Pattern Detection](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-detection)
    * [HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd)
    * [HODMD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hodmd)
    * [Low Cost Algorithms](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hodmd)
        - [Low Cost SVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#low-cost-svd)
        - [Low Cost HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#low-cost-hosvd)
        - [Low Cost HODMD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#low-cost-hodmd)

2. [Spatial Resolution Enhancement](https://modelflows.github.io/modelflowsapp/modaldecomposition/#spatial-resolution-enhancement)
    * [Gap Filling Tool](https://modelflows.github.io/modelflowsapp/modaldecomposition/#gap-filling-tool)
    * [Superresolution Tool](https://modelflows.github.io/modelflowsapp/modaldecomposition/#superresolution-tool)

3. [Control](https://modelflows.github.io/modelflowsapp/modaldecomposition/#control)
   * [Passive Flow Control](https://modelflows.github.io/modelflowsapp/modaldecomposition/#passive-flow-control)



## Pattern Detection <a id="pattern-detection"></a>

### Higher Order Singular Value Decomposition (HOSVD) <a id="pattern-hosvd"></a>

HOSVD, or High Order Singular Value Decomposition, is a mathematical technique used in pattern detection and analysis for high-dimensional data. HOSVD can be used to decompose a high-dimensional tensor into a set of orthogonal rank-1 tensors, which represent the underlying patterns in the data. The technique allows for the extraction of features that are relevant for further analysis, such as the spatiotemporal behavior of a system.

HOSVD has been used in various fields, including image and signal processing, and has gained attention in fluid mechanics for pattern detection. By applying HOSVD to flow data, researchers can identify patterns related to vortices, turbulence, and other important fluid flow phenomena. HOSVD can also be used in combination with other techniques, such as machine learning algorithms or HODMD, to enhance the accuracy and predictive power of the analysis.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/hosvd.png?raw=true)

The following video explains how this algorithm is applied:

<iframe width="560" height="315" src="https://www.youtube.com/embed/3DzDHSrZtYA?si=fGOXS4YYKOeKZ-q4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

More details can be found in the book:

[*J.M. Vega & S. Le Clainche, " Higher Order Dynamic Mode Decomposition and Its Applications", Academic Press, Elsevier, 2020, ISBN 9780128197431.*](https://www.sciencedirect.com/book/9780128197431/higher-order-dynamic-mode-decomposition-and-its-applications)

And application of the code in:
[*Lazpita, E., Martínez-Sánchez, Á., Corrochano, A., Hoyas, S., Le Clainche, S., & Vinuesa, R. (2022). On the generation and destruction mechanisms of arch vortices in urban fluid flows. Physics of Fluids, 34(5).*](https://doi.org/10.1063/5.0088305)

Download the code for **HOSVD** in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/hosvd.zip),
in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/hosvd.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/hosvd.ipynb).


### Higher Order Dynamic Mode Decomposition (HODMD) <a id="pattern-hodmd"></a>

HODMD, or Higher Order Dynamic Mode Decomposition, is a mathematical technique used to analyze complex dynamical systems. It has gained attention in the fluid mechanics community as a powerful tool for pattern detection. HODMD enables the decomposition of high-dimensional data into a set of dynamic modes that represent spatiotemporal patterns in the data. These dynamic modes are computed by solving an optimization problem, which identifies the most relevant temporal and spatial patterns in the data. Once the dynamic modes have been computed, they can be used to perform a variety of analyses, including mode stability analysis, mode mixing analysis, and prediction of future behavior. By applying HODMD to flow data, researchers can identify patterns related to vortex shedding, boundary layer separation, and other important fluid flow phenomena.

HODMD is also applicable to other complex dynamical systems such as chemical reactions, biological processes, and weather patterns. Its ability to extract dynamic modes from high-dimensional datasets makes it a valuable tool for analyzing complex systems that are difficult to understand using traditional analysis techniques. The use of HODMD in combination with other methods, such as machine learning algorithms, can enhance the accuracy and predictive power of the analysis. As such, HODMD is an exciting and promising technique for pattern detection and analysis in a variety of fields, including fluid mechanics.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/HODMDcalibration.png?raw=true)

The following video explains how this algorithm is applied:

<iframe width="560" height="315" src="https://www.youtube.com/embed/RYyPlpjD3PU?si=kc7jAd69KQz35bXK" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

The following book details several applications of HODMD for pattern identification, temporal forecasting, data reconstruction, etc. The book also includes the [Matlab codes](https://data.mendeley.com/datasets/z8ks4f5vy5/1) and some test databases:

[*J.M. Vega & S. Le Clainche, " Higher Order Dynamic Mode Decomposition and Its Applications", Academic Press, Elsevier, 2020, ISBN 9780128197431.*](https://www.sciencedirect.com/book/9780128197431/higher-order-dynamic-mode-decomposition-and-its-applications)

And the application of the code in:
[*Lazpita, E., Martínez-Sánchez, Á., Corrochano, A., Hoyas, S., Le Clainche, S., & Vinuesa, R. (2022). On the generation and destruction mechanisms of arch vortices in urban fluid flows. Physics of Fluids, 34(5).*](https://doi.org/10.1063/5.0088305)

Download the code for **standard HODMD** in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/hodmd.zip),
in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/hodmd.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/hodmd.ipynb).

Download the code for **multi-dimensional iterative HODMD** in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/mdhodmd.zip),
in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/mdhodmd.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/mdhodmd.ipynb).


### Low Cost Algorithms <a id="low-cost"></a>

#### Low Cost SVD <a id="low-cost-svd"></a>
Low-cost singular value decomposition (LC-SVD) is a modal decomposition-based database reconstruction method used to enhance the resolution of optimally sampled experimental data using data assimilation. To achieve so, LC-SVD first uses [pysensors](https://arxiv.org/abs/2102.13476), to identify the optimal sensor positions for a reduced (or available) number of sensors, ensuring that the most critical flow patterns are captured over time. The coordinates of these sensors are then used to collect experimental data optimally. Once the experimental data has been stored, LC-SVD is applied to enhance the resolution of the POD modes and temporal coefficients' matrices, fusing the experimental database and its corresponding high-resolution numerical simulation. These reconstructed matrices are then used to reconstruct the high-resolution snapshots tensor. This novel method makes it possible to enhance the resolution of experimental data 50000 times its original size, 123 times faster than standard SVD, using 40% less memory, achieving in some cases reconstruction errors close to 0.5%.    

![Low-cost Singular Value Decomposition methodology summary](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/LC-SVD.jpg?raw=true)

[Hetherington, Ashton, and Soledad Le Clainche. "Low-cost singular value decomposition with optimal sensor placement." *arXiv preprint* arXiv:2311.09791 (2023)](https://arxiv.org/abs/2311.09791)

Download the code for **low-cost SVD** in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/Low-cost-singular-value-decomposition.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/modal-decomposition/python/Low-cost-singular-value-decomposition.ipynb).

#### Low Cost HODMD <a id="low-cost-hodmd"></a>
Large and complex datasets often present computational challenges, particularly when using standard Singular Value Decomposition (SVD). As dataset sizes grow, the scalability of conventional SVD becomes a major bottleneck, especially in applications requiring repeated computations.

To address this, Low-Cost Higher Order Dynamic Mode Decomposition (lcHODMD) extends standard HODMD with a more efficient approach that reduces both memory usage and computational time. This method leverages either Low-Cost Singular Value Decomposition (lcSVD) or Low-Cost Higher Order Singular Value Decomposition (lcHOSVD) to enhance scalability and performance.


Reference us with:

ModelFLOWs (2023). *ModelFLOWs-app*. Retrieved [date], from [https://modelflows.github.io/modelflowsapp/](https://modelflows.github.io/modelflowsapp/)

<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) --> 
*Code in progress. Coming soon...*



## Spatial Resolution Enhancement <a id="spatial-resolution-enhancement"></a>

### Gap Filling Tool <a id="gap-filling-tool"></a>
Gappy filling is a technique used to fill in missing or incomplete data points in a dataset, using various methods such as linear regression, interpolation, and extrapolation. The goal is to reconstruct a complete dataset that can be analyzed using traditional analysis techniques. The gappy filling tool aims to reconstruct the missing data points.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Gappy.png?raw=true)

Application in complex databases:

[Tagilaferro, S., Corrochano, A., Marchetti, P., Marcon, A., Le Clainche, S., A new method based on physical patterns to impute aerobiological datasets, PLoS ONE 19(11): e0314005, 2024.](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0314005)

Download the code for **Gap Filling Tool**  in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/hosvd_gappy_Matlab.zip), in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/hosvd_gappy.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/hosvd_gappy.ipynb).


### Superresolution Tool <a id="superresolution-tool"></a>
The super-resolution tool, based on SVD, is a technique used to improve the quality of a dataset that contains incomplete or noisy data. This technique involves using statistical methods to identify and remove noise from the data or to fill in missing data points with more accurate estimates. The goal is to produce a more accurate and reliable dataset that can be used for further analysis. The superresolution tool aims to improve the overall quality of the dataset.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/SuperTool.png?raw=true)

Application in complex problems:

[Hetherington, A., Serfaty, D., Corrochano, A., Soria, J., Le Clainche, S., Data repairing and resolution enhancement using data-driven modal decomposition and deep learning, Exp. Therm. Fluid  Sci., 157, 111241, 2024.](https://www.sciencedirect.com/science/article/pii/S0894177724001109)

Download the code for **Superresolution Tool**  in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/hosvd_superres_Matlab.zip), in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/hosvd_superres.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/hosvd_superres.ipynb).

## Control <a id="control"></a>

### Passive Flow Control <a id="passive-flow-control"></a>
Based on HODMD, ModelFLOWs has been able to create a fully data-driven algorithm to calculate the so-called *non-linear structural sensitivity*. 
This concept identifies the region in the spatial domain where the flow is most prone to changes. Therefore, it has applications in flow control, as perturbing this region with a punctual force or a small geometric modification may delay the onset of some instabilities.

In linear theory, it is possible to calculate the structural sensitivity, but it is necessary to combine direct and adjoint solutions, as well as linearising the Navier-Stokes Equations. In realistic problems, these calculations would be expensive in terms of computational memory and time.  Moreover, these algorithms cannot be applied to experiments or turbulent flows.

In the proposed method, any type of database (coming from experiments or numerical simulations) can be analyzed. The data-driven algorithm first filters the data in order to retain the most important dynamics. Then, the non-linear structural sensitivity can be calculated, using the DMD modes and the non-linear operator of the Navier-Stokes equations. A flow chart of the passive flow control process is shown below.

<img src="https://raw.githubusercontent.com/modelflows/modelflowsapp/master/assets/img/MDControl.png"
     alt="Figure text"
     style="visibility: visible;" />

For a proper usage of the algorithm, it is recommended to first calibrate the HODMD algorithm, following the [Advanced Tutorial](https://modelflows.github.io/modelflowsapp/advanced/) in our website.

[*Corrochano, A., Le Clainche, S., Structural sensitivity in non-linear flows using direct solutions, Computers & Mathematics with Applications, 2022.*](https://doi.org/10.1016/j.camwa.2022.10.006)

The following video explains how this algorithm is applied and the previous paper:

<iframe width="560" height="315" src="https://www.youtube.com/embed/fbd_loMGghs?si=NVipGqQ6BJH913vI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


Download the code for **Passive Flow Control**  in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/mdhodmd_control_Matlab.zip), in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/mdhodmd_control.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/mdhodmd_control.ipynb).
