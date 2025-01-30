---
layout: page
title: Deep Learning
<!-- subtitle: Our codes focused on deep learning -->
---

Codes available:
1. [Parametric Study](https://modelflows.github.io/modelflowsapp/deeplearning/#parametric-study)
    * [Multiparametric Tool](https://modelflows.github.io/modelflowsapp/deeplearning/#multiparametric-tool)

2. [Spatial Resolution Enhancement](https://modelflows.github.io/modelflowsapp/deeplearning/#spatial-resolution-enhancement)
    * [Superresolution Tool](https://modelflows.github.io/modelflowsapp/deeplearning/#superresolution-tool)

3. [Temporal Forecasting](https://modelflows.github.io/modelflowsapp/deeplearning/#temporal-forecasting)
    * [Hybrid Generative Model](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-generative-model)
        - [Standard](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-generative-standard)
        - [Advanced](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-generative-advanced)
    * [Full Deep Learning Generative Model](https://modelflows.github.io/modelflowsapp/deeplearning/#full-dl-generative-model)
        - [Residual](https://modelflows.github.io/modelflowsapp/deeplearning/#full-generative-residual)
        - [Variational](https://modelflows.github.io/modelflowsapp/deeplearning/#full-generative-variational)
    * [Hybrid Predictive Model](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model)
    * [Remote Sensing and DLinear](https://modelflows.github.io/modelflowsapp/deeplearning/#dlinear)

3. [Control](https://modelflows.github.io/modelflowsapp/deeplearning/#control)

## Parametric Study <a id="parametric-study"></a>

### Multiparametric Tool <a id="multiparametric-tool"></a>
Numerical simulations of complex fluid phenomena are computationally expensive in terms of computational resources and processing time. Several numerical simulations must be performed to analyze the behavior of the flow under different flow regimes or parameters, and this entire process can take several weeks or even months.

To overcome these limitations, we have developed an innovative tool capable of efficiently generating new fluid dynamics databases for specific flow conditions (parameters) and predicting their behavior over time. This is achieved using a hybrid, fully data-driven Reduced-Order Model (ROM), which combines Higher-Order Modal Decomposition (HOSVD) with Recurrent Neural Networks (RNN) and the Kriging interpolation method, also known as Gaussian Process Regression (GPR).

This framework has been developed using [Python]( https://www.python.org/)’s ML libraries, [Tensorflow]( https://www.tensorflow.org/)/[Keras]( https://www.tensorflow.org/guide/keras?hl=es-419), and the [PyKrige]( https://geostat-framework.readthedocs.io/projects/pykrige/en/stable/index.html ) interpolation library. The tool has been tested on databases obtained through numerical simulations at different flow parameters, such as Reynolds number and Angle of Attack.

![Multi-parametric tool - Methodology](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_Barragan_multipar.png?raw=true)
*Work in progress. Coming soon...*


## Spatial Resolution Enhancement <a id="spatial-resolution-enhancement"></a>

### Superresolution Tool <a id="superresolution-tool"></a>
Fluid mechanics plays a significant role in most natural and anthropogenic processes. During the last decades, numerical methods such as the Finite Volume Method (FVM) have been widely used to predict the behavior of fluid dynamics phenomena. However, performing accurate numerical simulations for complex flows (such as those in a turbulent regime, multiphase flows, multiscale phenomena, etc.) demands significant computational resources in terms of processing and storage capacity and takes long periods of time to converge.

In order to overcome the limitations of conventional numerical solvers, a fully data-driven hybrid physics-based Reduced-Order Model (ROM) that combines modal decomposition methods and Machine Learning (ML) has been developed. This methodology combines Higher-Order Singular Value Decomposition ([HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd)) with fully connected neural networks (FCNN) to enhance the spatial resolution of a fluid dynamics database. [HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd) has demonstrated its capability of extracting the main patterns and structures of fluid dynamics phenomena while denoising and compressing the database, while Neural Networks are able to model the non-linearities. This framework has been developed using [Python]( https://www.python.org/)’s ML libraries [Tensorflow]( https://www.tensorflow.org/)/[Keras]( https://www.tensorflow.org/guide/keras?hl=es-419)

![Super resolution tool - Methodology ](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_Barragan_superresolution.png?raw=true)
*Work in progress. Coming soon...*


## Temporal Forecasting <a id="temporal-forecasting"></a>

### Hybrid Generative Model <a id="hybrid-generative-model"></a>

#### Standard <a id="hybrid-generative-standard"></a>
This model presents a hybrid ROM integrating Higher-Order Singular Value Decomposition (HOSVD) with Long Short-Term Memory (LSTM) architecture. The approach leverages a rolling window framework to extract temporal patterns. The LSTM model processes the sequences, capturing nonlinear dependencies and preserving long-term temporal correlations. Predictions are generated autoregressively, where forecasted snapshots are fed back as inputs to itteratively predict the next step. The integration of HOSVD enables dimensionality reduction, optimizing computational efficiency without compromising accuracy. While this approach can also be implemented with Singular Value Decomposition (SVD), HOSVD extends the capabilities of SVD by better preserving multi-dimensional structures, leading to improved performance in complex dynamical systems. This framework is implemented using TensorFlow/Keras for robust time-series forecasting applications.

![Figure text](https://github.com/modelflows/modelflowsapp/blob/d356b4aa65afd90fa0e8e1cba902d919b621e307/assets/img/2025_01_30_sengupta_Temporalforecasting.PNG?raw=true) 

#### Advanced <a id="hybrid-generative-advanced"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*


### Full Deep Learning Generative Model <a id="full-dl-generative-model"></a>

#### Residual <a id="full-generative-residual"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*

#### Variational <a id="full-generative-variational"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*


### Hybrid Predictive Model <a id="hybrid-predictive-model"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*


### Remote Sensing and DLinear <a id="dlinear"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*



## Control <a id="control"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*

