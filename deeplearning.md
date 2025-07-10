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
    * [Hybrid Predictive Model: POD-DL](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model)
        - [POD-DL: Fixed temporal horizon](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model-fixed-h)
        - [POD-DL: Autoregressive](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model-ar)
   * [Hybrid Predictive Model: HOSVD-DL](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model)
        - [HOSVD-DL: Autoregressive](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model-ar)
    * [Remote Sensing and DLinear](https://modelflows.github.io/modelflowsapp/deeplearning/#dlinear)
    * [Deep Learning Models](https://modelflows.github.io/modelflowsapp/deeplearning/#full-dl-generative-model)
        - [Residual Autoencoder (point forecasting)](https://modelflows.github.io/modelflowsapp/deeplearning/#full-generative-residual)
        - [Variational Autoencoder (probabilistic forecasting)](https://modelflows.github.io/modelflowsapp/deeplearning/#full-generative-variational)
4. [Adaptive Methodology](https://modelflows.github.io/modelflowsapp/deeplearning/#adaptive-methodology)
5. [Control](https://modelflows.github.io/modelflowsapp/deeplearning/#control)

## Parametric Study <a id="parametric-study"></a>

### Multiparametric Tool <a id="multiparametric-tool"></a>
## Hybrid Data-Driven Reduced-Order Modeling for Fluid Dynamics

Numerical simulations of complex fluid phenomena are computationally expensive in terms of resources and processing time. Multiple simulations are typically required to analyze flow behavior under various regimes or parameters, an effort that can span several weeks or even months.

To address these challenges, we have developed an innovative tool capable of efficiently generating new fluid dynamics databases for specific flow conditions and predicting their temporal evolution. This is achieved using a hybrid, fully data-driven Reduced-Order Model (ROM), which integrates:

- **Higher-Order Singular Value Decomposition (HOSVD)** for modal decomposition,
- **Recurrent Neural Networks (RNN)** for temporal prediction,
- **Gaussian Process Regression (GPR)** for parameter-space interpolation.

The framework is implemented using:

- [Python](https://www.python.org/)
- [PyTorch](https://pytorch.org/) for deep learning (RNN)
- [scikit-learn](https://scikit-learn.org/stable/modules/gaussian_process.html) for GPR-based interpolation

This tool has been validated on datasets obtained from numerical simulations at varying flow parameters such as Reynolds number and Angle of Attack.


![Multi-parametric tool - Methodology](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_Barragan_multipar.png?raw=true)

Download the code [*here*](https://github.com/modelflows/notebooks/raw/main/deep-learning/Multiparametric.zip) or the Jupyter notebook [*here*](https://github.com/modelflows/notebooks/raw/main/deep-learning/Multiparametric.zip)

Download the databases [*here*]()

## Spatial Resolution Enhancement <a id="spatial-resolution-enhancement"></a>

### Superresolution Tool <a id="superresolution-tool"></a>
Fluid mechanics plays a significant role in most natural and anthropogenic processes. During the last decades, numerical methods such as the Finite Volume Method (FVM) have been widely used to predict the behavior of fluid dynamics phenomena. However, performing accurate numerical simulations for complex flows (such as those in a turbulent regime, multiphase flows, multiscale phenomena, etc.) demands significant computational resources in terms of processing and storage capacity and takes long periods of time to converge.

In order to overcome the limitations of conventional numerical solvers, a fully data-driven hybrid physics-based Reduced-Order Model (ROM) that combines modal decomposition methods and Machine Learning (ML) has been developed. This methodology combines Higher-Order Singular Value Decomposition ([HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd)) with fully connected neural networks (FCNN) to enhance the spatial resolution of a fluid dynamics database. [HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd) has demonstrated its capability of extracting the main patterns and structures of fluid dynamics phenomena while denoising and compressing the database, while Neural Networks are able to model the non-linearities. This framework has been developed using [Python]( https://www.python.org/)’s ML libraries [Tensorflow]( https://www.tensorflow.org/)/[Keras]( https://www.tensorflow.org/guide/keras?hl=es-419)

![Super resolution tool - Methodology ](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_Barragan_superresolution.png?raw=true)

Download the code [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/SUPERRESOLUTION.zip).  -->

## Temporal Forecasting <a id="temporal-forecasting"></a>

### Hybrid Predictive Model: POD-DL <a id="hybrid-predictive-model"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
The POD-DL model is a hybrid approach that integrates proper orthogonal decomposition (POD) with deep learning (DL) architectures, primarily an LSTM, to forecast the temporal evolution of flow dynamics. It follows an encoder-decoder structure, where the encoder corresponds to the matrix decomposition performed by POD, encapsulating the POD modes and coefficients. Since the temporal dynamics are encoded in the POD coefficients, the DL architecture focuses solely on forecasting these coefficients, while the POD modes remain unchanged. Once the new coefficients are computed, the decoder reconstructs the flow field by reversing the POD decomposition, i.e., performing a matrix multiplication. This process yields snapshots corresponding to future flow dynamics.

The forecasting can be conducted using either a [fixed temporal horizon](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model-fixed-h), where the model predicts a predetermined number of snapshots simultaneously, or an [autoregressive](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model-ar) approach, where multiple predictions are iteratively computed by feeding previously generated outputs back into the model.

The POD-DL model can process datasets represented as tensors of either four or five dimensions, structured as [C,X,Y,Z,T]. Here, C denotes the dataset components, such as different velocity components, Reynolds numbers, or initial conditions. The indices X, Y and Z correspond to the spatial discretization along the x-, y- and z-axis, respectively, while T represents the temporal dimension, indicating the number of snapshots. For four-dimensional tensors, the Z index may either be absent or set to Z = 1. <ins>Datasets with higher or lower dimensionality, or with a different arrangement of dimensions, may result in errors when executing the codes</ins>.

For example these codes can be tested with either the dataset corresponding to the two-dimensional laminar flow past a cylinder, which is available [here](https://modelflows.github.io/modelflowsapp/databases/#cylinder-2d), or the three-dimensional laminar flow past a cylinder, which is available [here](https://modelflows.github.io/modelflowsapp/databases/#cylinder-3d-long). Also note these models require a CPU for training.

#### POD-DL: Fixed temporal horizon <a id="hybrid-predictive-model-fixed-h"></a>
![Figure pod_dl_fixed_horizon](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_AbadiaHeredia_POD_DL_Orig.png?raw=true)

[R. Abadía-Heredia, M. López-Martín, B. Carro, J. Arribas, J. Pérez, and S. Le Clainche, “A predictive hybrid reduced order model based on proper orthogonal decomposition combined with deep learning architectures,” Expert Systems with Applications 187, 115910 (2022).](https://doi.org/10.1016/j.eswa.2021.115910)

Download the code [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/pod_dl_fixed_h.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/pod_dl_fixed_h.ipynb).

#### POD-DL: Autoregressive <a id="hybrid-predictive-model-ar"></a>
![Figure pod_dl_ar](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_AbadiaHeredia_ARmodels_POD_DL.png?raw=true)

[R. Abadía-Heredia, A.Corrochano, M. López-Martín and S. Le Clainche, “Generalization capabilities and robustness of hybrid machine learning models grounded in flow physics compared to purely deep learning models,” Physics of Fluids 37, 035149 (2025).](https://doi.org/10.1063/5.0253876)

Download the code [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/dl_ar_models.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/modelFlows_ar_pod_dl.ipynb).

### Hybrid Predictive Model: HOSVD-DL <a id="hybrid-predictive-model"></a>
This model presents a hybrid ROM integrating Higher Order Singular Value Decomposition ([HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd)) with Long Short Term Memory (LSTM) architecture for temporal predictions. The integration of [HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd) enables dimensionality reduction and the LSTM model processes the sequences, capturing nonlinear dynamics and preserving long-term temporal correlations. Predictions are generated autoregressively, where forecasted solutions are fed back as inputs to itteratively predict the next step.  While this approach can also be implemented with Singular Value Decomposition (SVD),  [HOSVD](https://modelflows.github.io/modelflowsapp/modaldecomposition/#pattern-hosvd) extends the capabilities of SVD by better preserving multi-dimensional structures, leading to improved performance in complex dynamical systems. This framework is implemented using TensorFlow/Keras for 4D and 5D tensors.
#### HOSVD-DL: Autoregressive <a id="hybrid-predictive-model-ar"></a>
![Figure text](https://github.com/modelflows/modelflowsapp/blob/d356b4aa65afd90fa0e8e1cba902d919b621e307/assets/img/2025_01_30_sengupta_Temporalforecasting.PNG?raw=true) 
[A. Sengupta, R. Abadía-Heredia, A. Hetherington, J. Miguel Perez, S. Le Clainche - " Hybrid machine learning models based on physical patterns to accelerate CFD simulations: a short guide on autoregressive models," arXiv:2504.06774 (2025).](https://doi.org/10.48550/arXiv.2504.06774)

To run it in *Colab*, or to download the codes click [*here*](https://drive.google.com/drive/folders/1BLRw6WsNC451o9shnhw7gf-Q8OtBmcpo) 



### Remote Sensing and DLinear <a id="dlinear"></a>
LC-SVD-DLinear (and LC-HOSVD-DLinear) are two hybrid machine learning models that combine [low-cost singular value decomposition (LC-SVD)](https://modelflows.github.io/modelflowsapp/modaldecomposition/#low-cost-svd) and [low-cost high-order singular value decomposition](https://modelflows.github.io/modelflowsapp/modaldecomposition/#low-cost-hosvd) with the DLinear architecture to efficiently forecast high-resolution experimental data collected from optimally placed sensors. These models operate by first using LC-SVD or LC-HOSVD to break down the experimental data and up-sample the temporal coefficients, POD modes, and singular values, significantly reducing computational cost while retaining all physical information. The reconstructed temporal coefficients are then processed by the DLinear model, which decomposes them into trend and seasonality components to identify temporal patterns and predict future values autoregressively, using the sliding window mechanism. Finally, the predicted temporal coefficients are combined with the reconstructed POD modes and singular values to generate high-resolution forecast snapshots, ensuring both accuracy and efficiency in handling complex, high-dimensional data.

![LC-SVD-DLinear architecture summary](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/LC-SVD-DLinear.jpg?raw=true) 

[Hetherington, A., Leonés, J. L., & Clainche, S. L. (2024). LC-SVD-DLinear: A low-cost physics-based hybrid machine learning model for data forecasting using sparse measurements. arXiv preprint arXiv:2411.17433.](https://arxiv.org/abs/2411.17433)

Download the code for **SVD-DLinear** in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/SVD-DLinear.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/SVD-DLinear.ipynb).  
Download the code for **LC-SVD-DLinear** in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/LC-SVD-DLinear.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/LC-SVD-DLinear.ipynb).  
Download the code for **HOSVD-DLinear** in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/HOSVD-DLinear.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/HOSVD-DLinear.ipynb). 
Download the code for **LC-HOSVD-DLinear** in Python version [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/LC-HOSVD-DLinear.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/LC-HOSVD-DLinear.ipynb). 

### Deep Learning Models <a id="full-dl-generative-model"></a>

Forecasting models for fluid dynamics that rely entirely on deep learning are typically built using convolutional neural networks (CNNs). This is because datasets describing flow dynamics consist of two-dimensional or three-dimensional snapshots that encode the spatiotemporal characteristics of the flow. In this context, an autoencoder, where both the encoder and decoder are implemented with CNNs, enables efficient processing of the spatial dimensions of the dataset. 

Specifically, the encoder constructs a latent representation that may capture key flow structures. Forecasting is then performed within this latent space, commonly using a convolutional long short-term memory (ConvLSTM) network. The predicted latent variables are subsequently passed through the decoder to reconstruct the snapshots corresponding to future flow dynamics.

Forecasting can be broadly categorized into two main types: [point forecasting](https://modelflows.github.io/modelflowsapp/deeplearning/#full-generative-residual) and [probabilistic forecasting](https://modelflows.github.io/modelflowsapp/deeplearning/#full-generative-variational). Point forecasting approximates a deterministic function that describes the prediction process, whereas probabilistic forecasting estimates the underlying probability distribution of the forecast. A Residual Autoencoder is employed for point forecasting, while a Variational Autoencoder (VAE) is used for probabilistic forecasting.

Both the Residual Autoencoder and the VAE are autoregressive and they can process datasets in a five-dimensional tensor format, structured as [C,X,Y,Z,T]. Here, C denotes the dataset components, such as different velocity components, Reynolds numbers, or initial conditions. The indices X, Y and Z correspond to the spatial discretization along the x-, y- and z-axis, respectively, while T represents the temporal dimension, indicating the number of snapshots.

Unlike the [POD-DL](https://modelflows.github.io/modelflowsapp/deeplearning/#hybrid-predictive-model) model, the architectures of these models are inherently dependent on the shape of the input snapshots. For the codes available on this page, the dataset must adhere to the following dimensional constraints: C = 3, X = 100, Y = 40, and Z = 64, with T remaining variable. <ins>Datasets with higher or lower dimensionality, or with a different arrangement of dimensions, may result in errors when executing the codes</ins>.

For example, these codes can be tested with the dataset corresponding to the two-dimensional laminar flow past a cylinder, which is available [here](https://modelflows.github.io/modelflowsapp/databases/#cylinder-2d). Also note these models require a GPU for training.

#### Residual Autoencoder (point forecasting) <a id="full-generative-residual"></a>
![Figure pod_dl_fixed_horizon](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_AbadiaHeredia_ARmodels_Res_AE.png?raw=true)

[R. Abadía-Heredia, A.Corrochano, M. López-Martín and S. Le Clainche, “Generalization capabilities and robustness of hybrid machine learning models grounded in flow physics compared to purely deep learning models,” Physics of Fluids 37, 035149 (2025).](https://doi.org/10.1063/5.0253876)

Download the code [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/dl_ar_models.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/modelFLows_ar_res_conv_ae.ipynb).

#### Variational Autoencoder (probabilistic forecasting) <a id="full-generative-variational"></a>
![Figure pod_dl_fixed_horizon](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_01_30_AbadiaHeredia_ARmodels_VAE.png?raw=true)

[R. Abadía-Heredia, A.Corrochano, M. López-Martín and S. Le Clainche, “Generalization capabilities and robustness of hybrid machine learning models grounded in flow physics compared to purely deep learning models,” Physics of Fluids 37, 035149 (2025).](https://doi.org/10.1063/5.0253876)

Download the code [*here*](https://github.com/modelflows/notebooks/raw/refs/heads/main/deep-learning/dl_ar_models.zip) or open it in [*Colab*](https://github.com/modelflows/notebooks/blob/main/deep-learning/modelFlows_ar_vae.ipynb).

## Adaptive Methodology <a id="adaptive-methodology"></a>

The use of fully data-driven models to modelize flow dynamics is a challenging task due to the apperance of distribution shifts within the dynamics. Data-driven models are allways trained on a dataset representing a certain distribution, if the real dynamics to be predicted start to deviate from the training distribution (e.g., due to a change of flow regime, the apperance of a new attractor, etc.), the model would not be able to predict this unseen variation, making the prediction unaccurate. Therefore, an adaptive methodology was proposed to couple traditional numerical solvers (costly, but highly accurate) with deep learning models (cheap, but less accurate) to simulate the dynamics of a fluid for a long-term temporal horizon.

![Figure adaptive_methodology](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/adaptive_methodology.png?raw=true)

The code available for now in ModelFlows-app correspond to the official implementation of the work from [R. Abadia-Heredia *et.al.* 2025](https://arxiv.org/abs/2505.01531), which presents a proof of concept for this adaptive methodology combining datasets obtained from high-fidelity numerical simulations and experiments, with the POD-DL model. A work showing a real application of this adaptive methodology, by coupling the POD-DL model with a numerical solver is under review and will be uploaded to this site soon.

[R. Abadía-Heredia, M. López-Martín and S. Le Clainche, “An Adaptive Framework for Autoregressive Forecasting in CFD Using Hybrid Modal Decomposition and Deep Learning,” arXiv preprint 	arXiv:2505.01531 (2025).](https://doi.org/10.48550/arXiv.2505.01531)

Check the official GitHub [*repository*](https://github.com/RAbadiaH/adaptive-cfd-forecasting-hybrid-modal-decomposition-deep-learning.git) or download it [*here*.](https://github.com/RAbadiaH/adaptive-cfd-forecasting-hybrid-modal-decomposition-deep-learning/archive/refs/heads/main.zip)

## Control <a id="control"></a>
<!-- Short description of the method. -->
<!-- ![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/YOURIMAGEHERE.png?raw=true) -->
*Work in progress. Coming soon...*

