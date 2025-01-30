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

2. [Spatial Resolution Enhancement](https://modelflows.github.io/modelflowsapp/deeplearning/#spatial-resolution-enhancement)
    * [Gap Filling Tool](https://modelflows.github.io/modelflowsapp/deeplearning/#gap-filling-tool)
    * [Superresolution Tool](https://modelflows.github.io/modelflowsapp/deeplearning/#superresolution-tool)

3. [Control](https://modelflows.github.io/modelflowsapp/modaldecomposition/#control)
   * [Passive FlowControl](https://modelflows.github.io/modelflowsapp/modaldecomposition/#passive-flow-control)



## Pattern Detection <a id="pattern-detection"></a>

### Higher Order Singular Value Decomposition (HOSVD) <a id="pattern-hosvd"></a>

The Higher-Order Singular Value Decomposition (HOSVD) is a generalization of the standard SVD to tensors, enabling the decomposition of multi-dimensional data into a core tensor and orthonormal factor matrices along each mode. This method is widely used in modal decomposition, data compression, and feature extraction, particularly in fields dealing with high-dimensional datasets such as fluid dynamics and biomedical imaging. By capturing dominant structures in data, HOSVD facilitates reduced-order modeling and pattern recognition while preserving key spatial and temporal correlations.

<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->

*Work in progress. Coming soon...*


### Higher Order Dynamic Mode Decomposition (HODMD) <a id="pattern-hodmd"></a>

The Higher-Order Dynamic Mode Decomposition (HODMD) extends the traditional DMD to handle high-dimensional and multiway data efficiently by leveraging tensor decomposition techniques. 
By applying HOSVD as a preprocessing step, HODMD reduces noise sensitivity and improves the extraction of dominant spatiotemporal modes in complex dynamical systems. 
This makes it particularly useful for analyzing fluid flows, biomedical signals, and other time-dependent datasets, enabling reduced-order modeling and predictive analysis while maintaining the underlying system dynamics.

<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->

*Work in progress. Coming soon...*


### Low Cost Algorithms <a id="low-cost"></a>

#### Low Cost SVD <a id="low-cost-svd"></a>
Low-cost singular value decomposition (LC-SVD) is a modal decomposition-based database reconstruction method used for enhancing the resolution of optimally sampled experimental data using data assimilation. To achieve so, LC-SVD first uses [pysensors](https://arxiv.org/abs/2102.13476), to identify the optimal sensor positions for a reduced (or available) number of sensors, ensuring that the most critical flow patterns are captured over time. The coordinates of these sensors are then used to collect experimental data optimally. Once the experimental data has been stored, LC-SVD is applied to enhance the resolution of the POD modes and temporal coefficients matrices, fusing the experimental database an its corresponding high-resolution numerical simulation. These reconstruced matrices are then used to reconstruct the high-resolution snapshots tensor. This novel method makes it possible to enhance the resolution of experimental data 50000 times its original size, 123 times faster than standard SVD, using 40% less memory, achieving in some cases reconstruction errors close to 0.5%.    

[Low-cost Singular Value Decomposition methodology summary](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/LC-SVD.jpg?raw=true) --> 

#### Low Cost HOSVD <a id="low-cost-hosvd"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) --> 
*Work in progress. Coming soon...*

#### Low Cost HODMD <a id="low-cost-hodmd"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) --> 
*Work in progress. Coming soon...*



## Spatial Resolution Enhancement <a id="spatial-resolution-enhancement"></a>

### Gap Filling Tool <a id="gap-filling-tool"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*

### Superresolution Tool <a id="superresolution-tool"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*



## Control <a id="control"></a>

### Passive Flow Control <a id="passive-flow-control"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->


