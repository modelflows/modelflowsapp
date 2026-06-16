---
layout: page
topic: "Modal Decomposition"
tldr: "Tools to identify coherent structures and patterns in fluid dynamics."
title: Modal Decomposition
<!--subtitle: GENERAL SUBTITLE -->
---

Codes available:
1. [Pattern Detection](#pattern-detection)
    * [HOSVD](#pattern-hosvd)
    * [HODMD](#pattern-hodmd)
    * [Spatio Temporal Koopman Decomposition (STKD)](#STKD)
    * [Low-cost Algorithms](#low-cost)
        - [Low-cost SVD](#low-cost-svd)
        - [Low-cost HOSVD](#low-cost-hosvd)
        - [Low-cost HODMD](#low-cost-hodmd)

2. [Spatial Resolution Enhancement](#spatial-resolution-enhancement)
    * [Gap Filling Tool](#gap-filling-tool)
    * [Superresolution Tool](#superresolution-tool)

3. [Control](#control)
   * [Passive Flow Control with HODMD](#passive-flow-control-with-hodmd)
   * [Passive Flow Control with Resolvent Analysis](#passive-flow-control-with-resolvent-analysis)



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

### Spatio Temporal Koopman Decomposition (STKD) <a id="STKD"></a>
The Spatio-Temporal Koopman Decomposition (STKD) extends the High-Order Dynamic Mode Decomposition (HODMD) by enabling spatio-temporal analysis of multidimensional data. It represents spatio-temporal fields as combinations of traveling wave modes, each characterized by specific wavenumbers and spatial growth rates, forming intricate standing or propagating patterns. STKD accommodates expansions along multiple spatial dimensions, allowing complex dynamics to be captured across directions such as spanwise and streamwise.In the context of traveling waves, this decomposition allows us to describe how spatial patterns evolve over time in terms of their fundamental modes.STKD analysis helps us understand

a) Dominant Wavenumbers and Frequencies: Identifying which spatial wavenumbers and temporal frequencies dominate the dynamics.
b) Growth and Decay: Modes with positive/negative growth rates  indicate whether a wave pattern is amplifying or decaying over time.

![Flowchart1](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_pillai_stkd.png?raw=true)

[Le Clainche, S., Vega, J.M., ‘Spatio-Temporal Koopman Decomposition’, J. of Nonlin. Sci. Vol. 28 (3), 1-50, 2018 ](https://link.springer.com/article/10.1007/s00332-018-9464-z)

Application to identify flow instabilitites:
[Le Clainche, S., Izbassarov, D., Rosti, M., Brandt, L., & Tammisola, O. (2020). Coherent structures in the turbulent channel flow of an elastoviscoplastic fluid. Journal of Fluid Mechanics, 888, A5.](https://www.researchgate.net/publication/338544827_Coherent_structures_in_the_turbulent_channel_flow_of_an_elastoviscoplastic_fluid)

Download the code for **STKD** in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/stkd.zip).


### Low-cost Algorithms <a id="low-cost"></a>

#### Low-cost SVD <a id="low-cost-svd"></a>
Low-cost singular value decomposition (LC-SVD) is a modal decomposition-based database reconstruction method used to enhance the resolution of optimally sampled experimental data using data assimilation. To achieve so, LC-SVD first uses [pysensors](https://arxiv.org/abs/2102.13476), to identify the optimal sensor positions for a reduced (or available) number of sensors, ensuring that the most critical flow patterns are captured over time. The coordinates of these sensors are then used to collect experimental data optimally. Once the experimental data has been stored, LC-SVD is applied to enhance the resolution of the POD modes and temporal coefficients' matrices, fusing the experimental database and its corresponding high-resolution numerical simulation. These reconstructed matrices are then used to reconstruct the high-resolution snapshots tensor. This novel method makes it possible to enhance the resolution of experimental data 50000 times its original size, 123 times faster than standard SVD, using 40% less memory, achieving in some cases reconstruction errors close to 0.5%.    

![Low-cost Singular Value Decomposition methodology summary](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/LC-SVD.jpg?raw=true)

[Hetherington, Ashton, and Soledad Le Clainche. "Low-cost singular value decomposition with optimal sensor placement." *arXiv preprint* arXiv:2311.09791 (2023)](https://arxiv.org/abs/2311.09791)

Download the code for **low-cost SVD** in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/Low-cost-singular-value-decomposition.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/modal-decomposition/python/Low-cost-singular-value-decomposition.ipynb).

#### Low-cost HOSVD <a id="low-cost-hosvd"></a>

Low-cost High Order Singular Value Decomposition (LC-HOSVD) extends the low-cost modal reconstruction idea to multidimensional tensor databases. Unlike standard SVD, where the dataset is reshaped into a matrix, LC-HOSVD preserves the natural tensor structure of the data. This is especially useful for flow databases arranged in several dimensions, such as spatial directions, physical variables, parameters, and time. The method first selects a reduced set of representative sensor locations from the original high-resolution database. These sparse measurements are then used to build a reduced tensor. HOSVD is applied along the relevant tensor directions, producing compact mode matrices and a core tensor. The retained modes are finally used to reconstruct the high-resolution database while keeping the multidimensional structure of the original problem. LC-HOSVD is particularly suitable for large 3D, 4D, and 5D databases, where preserving directional information is important. In urban flow applications, this allows the reconstruction of velocity, pressure, turbulence quantities, and pollutant concentration fields from a reduced number of sensor points. Compared with matrix-based LC-SVD, LC-HOSVD can better capture directional dependencies and localized three-dimensional structures, although it generally requires a higher computational cost.

<!-- ![Low-cost Higher Order Singular Value Decomposition methodology summary](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/LC-HOSVD.jpg?raw=true) -->

*Figure in progress. Coming soon...*

Reference us with:

ModelFLOWs (2023). *ModelFLOWs-app*. Retrieved [date], from [https://modelflows.github.io/modelflowsapp/](https://modelflows.github.io/modelflowsapp/)

*Reference in progress. Coming soon...*

*Code in progress. Coming soon...*

#### Low-cost HODMD <a id="low-cost-hodmd"></a>

Low-cost Higher Order Dynamic Mode Decomposition (LC-HODMD) is a dynamic reconstruction method designed for large time-resolved databases. It combines the low-cost reconstruction philosophy with Higher Order Dynamic Mode Decomposition, allowing the temporal behaviour of complex flow fields to be recovered from reduced or sparsely sampled data. The method first reduces the size of the original database using either LC-SVD or LC-HOSVD. This reduced representation is then used as the input for HODMD. The HODMD step requires the selection of key parameters, such as the delay dimension \(d\), the truncation tolerance \(\epsilon\), and the number of retained modes. These parameters control how much temporal memory is included and how many weak or noisy modes are discarded. After the reduced dynamic system is built, LC-HODMD extracts the dynamic modes, amplitudes, frequencies, and growth rates of the database. These quantities are then used to reconstruct the time-resolved flow field. In urban flow applications, LC-HODMD can be used to recover the temporal evolution of velocity, pressure, turbulent variables, and pollutant concentration fields while reducing memory usage and computational cost. This method is useful when the objective is not only to reconstruct a spatial field, but also to preserve its temporal dynamics. By combining low-cost reduction with HODMD, large time-dependent CFD datasets can be analysed more efficiently than with standard full-order HODMD.

<!-- ![Low-cost Higher Order Dynamic Mode Decomposition methodology summary](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/LC-HODMD.jpg?raw=true) -->

*Figure in progress. Coming soon...*

Reference us with:

ModelFLOWs (2023). *ModelFLOWs-app*. Retrieved [date], from [https://modelflows.github.io/modelflowsapp/](https://modelflows.github.io/modelflowsapp/)

*Reference in progress. Coming soon...*

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

### Passive Flow Control with HODMD <a id="passive-flow-control-with-hodmd"></a>
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


Download the code for **Passive Flow Control with HODMD**  in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/mdhodmd_control_Matlab.zip), in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/python/mdhodmd_control.zip),
or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/3dd21666bdc0777dcfe047fadf93d46053f975f9/modal-decomposition/python/mdhodmd_control.ipynb).

### Passive Flow Control with Resolvent Analysis <a id="passive-flow-control-with-resolvent-analysis"></a>
This study introduces a data-driven flow control tool based on resolvent analysis, designed to identify the most sensitive regions of a flow field, areas where small perturbations can produce large effects. Using modal decomposition techniques and the HODMD algorithm, the method extracts coherent structures and quantifies the input–output gain that governs flow amplification mechanisms.

The approach enables the detection of regions of high structural sensitivity without requiring linearization of the Navier–Stokes equations or adjoint computations, making it suitable for complex or experimental data.

Two test cases are demonstrated:
* Flow past a circular cylinder, where the tool identifies optimal positions to introduce small stabilizing cylinders that delay vortex shedding and flow instabilities.
* Turbulent channel flow with heat transfer, where resolvent analysis highlights sensitive areas for geometric modifications (ribs and cavities). The resulting configurations achieve enhanced heat transfer (≈ +10%) while reducing drag (≈ –6%), outperforming conventional designs.

This algorithm provides a powerful, fully data-driven framework for passive flow control, applicable to laminar and turbulent regimes alike.

<img src="https://raw.githubusercontent.com/modelflows/modelflowsapp/master/assets/img/ra.png"
     alt="Figure text"
     style="visibility: visible;" />

[*Lazpita, E., Garicano-Mena, J., Paniagua, G., Le Clainche, S., Valero, E., A data–driven sensibility tool for flow control based on resolvent analysis, Results in Engineering, 2024.*](https://www.sciencedirect.com/science/article/pii/S2590123024003244)

The following video explains how this algorithm is applied and the previous paper:

<iframe width="560" height="315" src="https://www.youtube.com/embed/y1DqWTl9FB0?si=5iUPbMpeTnQpSO-s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Download the code for **Passive Flow Control with Resolvent Analysis**  in MATLAB version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/ra.zip), or the version including HODMD [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/modal-decomposition/matlab/ra-hodmd.zip).

For a proper usage of the algorithm, it is recommended to first calibrate the HODMD algorithm, following the [Advanced Tutorial](https://modelflows.github.io/modelflowsapp/advanced/) in our website.

