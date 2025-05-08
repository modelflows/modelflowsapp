---
layout: page
title: Advanced tutorials
subtitle: How does each module work?
---

ModelFLOWs-app, an open source Software for data post-processing, patterns identification and development of reduced order models using modal decomposition and deep learning architectures. When using the software, please, reference us as: 

[*Hetherington, A., Corrochano, A., Abadía-Heredia, R., Lazpita, E., Muñoz, E., Díaz, P., ... & Le Clainche, S. (2024). ModelFLOWs-app: data-driven post-processing and reduced order modelling tools. Computer Physics Communications, 301, 109217.*](https://www.sciencedirect.com/science/article/pii/S0010465524001401)

This data-driven application consists of two modules: **Modal Decomposition** and **Deep Learning**. Both blocks consist of algorithms capable of **detecting patterns**, **reconstructing** and **predicting data** from complex flow databases.

The following video presents a clear overview of ModelFLOWs-app. 

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZKeShcM8nuI?si=jOUu3mio-dZYFxf5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Modal Decomposition
### Pattern detection
#### HODMD
HODMD, or Higher Order Dynamic Mode Decomposition, is a mathematical technique used to analyze complex dynamical systems. It has gained attention in the fluid mechanics community as a powerful tool for pattern detection. HODMD enables the decomposition of high-dimensional data into a set of dynamic modes that represent spatiotemporal patterns in the data. These dynamic modes are computed by solving an optimization problem, which identifies the most relevant temporal and spatial patterns in the data. Once the dynamic modes have been computed, they can be used to perform a variety of analyses, including mode stability analysis, mode mixing analysis, and prediction of future behavior. By applying HODMD to flow data, researchers can identify patterns related to vortex shedding, boundary layer separation, and other important fluid flow phenomena.

HODMD is also applicable to other complex dynamical systems such as chemical reactions, biological processes, and weather patterns. Its ability to extract dynamic modes from high-dimensional datasets makes it a valuable tool for analyzing complex systems that are difficult to understand using traditional analysis techniques. The use of HODMD in combination with other methods, such as machine learning algorithms, can enhance the accuracy and predictive power of the analysis. As such, HODMD is an exciting and promising technique for pattern detection and analysis in a variety of fields, including fluid mechanics.

ModelFLOWs-app presents two variants of HODMD: standard HODMD and iterative multi-dimensional HODMD (mdHODMD-it). Details about the main algorithms can be found in:

[*Le Clainche & Vega, Higher order dynamic mode decomposition, SIAM J. Appl. Dyn. Syst., 16(2), 882-925, 2017.*](https://epubs.siam.org/doi/10.1137/15M1054924)

[*Le Clainche, Vega & Soria, Higher order dynamic mode decomposition of noisy experimental data: The flow structure of a zero-net-mass-flux jet, Exp. Therm. and Fluid Sci., 88, 336-353, 2017.*](https://www.sciencedirect.com/science/article/abs/pii/S089417771730184X)

The following book details several applications of HODMD for patterns indentification, temporal forecasting, data reconstruction, etc. The book also includes the [Matlab codes](https://data.mendeley.com/datasets/z8ks4f5vy5/1) and some test databases:

[*J.M. Vega & S. Le Clainche, " Higher Order Dynamic Mode Decomposition and Its Applications", Academic Press, Elsevier, 2020, ISBN 9780128197431.*](https://www.sciencedirect.com/book/9780128197431/higher-order-dynamic-mode-decomposition-and-its-applications)

The following videos explains how this algorithm is applied using a classic and iterative approach:

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/HODMD-video.mp4?raw=true" type="video/mp4">
</video>

#### HOSVD
HOSVD, or High Order Singular Value Decomposition, is a mathematical technique used in pattern detection and analysis for high-dimensional data. HOSVD can be used to decompose a high-dimensional tensor into a set of orthogonal rank-1 tensors, which represent the underlying patterns in the data. The technique allows for the extraction of features that are relevant for further analysis, such as the spatiotemporal behavior of a system.

HOSVD has been used in various fields, including image and signal processing, and has gained attention in fluid mechanics for pattern detection. By applying HOSVD to flow data, researchers can identify patterns related to vortices, turbulence, and other important fluid flow phenomena. HOSVD can also be used in combination with other techniques, such as machine learning algorithms or HODMD, to enhance the accuracy and predictive power of the analysis. More details can be found in the book:

[*J.M. Vega & S. Le Clainche, " Higher Order Dynamic Mode Decomposition and Its Applications", Academic Press, Elsevier, 2020, ISBN 9780128197431.*](https://www.sciencedirect.com/book/9780128197431/higher-order-dynamic-mode-decomposition-and-its-applications)

The following video explains how this algorithm is applied:

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/HOSVD-video.mp4?raw=true" type="video/mp4">
</video>

### Reconstruction
#### Gappy data reconstruction and gappy data enhancement
Gappy data reconstruction and gappy data enhancement are two different techniques used to address different aspects of missing or incomplete data.

Gappy data reconstruction is a technique used to fill in missing or incomplete data points in a dataset, using various methods such as linear regression, interpolation, and extrapolation. The goal is to reconstruct a complete dataset that can be analyzed using traditional analysis techniques.

On the other hand, gappy data enhancement is a technique used to improve the quality of a dataset that contains incomplete or noisy data. This technique involves using statistical methods to identify and remove noise from the data, or to fill in missing data points with more accurate estimates. The goal is to produce a more accurate and reliable dataset that can be used for further analysis.

Both techniques are useful for dealing with incomplete or noisy data, but they address different aspects of the problem. Gappy data reconstruction aims to fill in missing data points, while gappy data enhancement aims to improve the overall quality of the dataset.

The following videos explain how these techniques are applied:

**Gappy data reconstruction**

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/GappySVD_Video.mp4?raw=true" type="video/mp4">
</video>

**Gappy data enhancement**

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/Enhancement_Video.mp4?raw=true" type="video/mp4">
</video>

### Prediction
#### HODMD
In fluid mechanics, predicting the behavior of complex flow systems is crucial for optimizing system performance and improving safety. Higher Order Dynamic Mode Decomposition (HODMD) is a powerful tool that can be used to make predictions about the future behavior of fluid flow systems based on past data. By identifying the most relevant spatiotemporal patterns in the flow data using HODMD, researchers can use these patterns to make accurate predictions about the future behavior of the system.

For example, HODMD can be used to identify the spatiotemporal patterns associated with vortices or turbulence in fluid flow. These patterns can then be used to predict the future behavior of the system, such as the development of vortices or turbulence at different times and locations. This information can be used to optimize system design, reduce energy consumption, and improve safety in a variety of fluid flow applications, such as aircraft design, combustion systems, and weather forecasting. More details can be found in the book:

[*J.M. Vega & S. Le Clainche, " Higher Order Dynamic Mode Decomposition and Its Applications", Academic Press, Elsevier, 2020, ISBN 9780128197431.*](https://www.sciencedirect.com/book/9780128197431/higher-order-dynamic-mode-decomposition-and-its-applications)

The following video explains how this algorithm is applied using a classic and iterative approach:

**Video coming soon**

## Deep Learning
### Pattern detection
Autoencoders are a powerful tool for pattern detection in fluid mechanics datasets using deep learning. An autoencoder is a neural network architecture that consists of an encoder and a decoder. The encoder compresses the input data into a low-dimensional representation, while the decoder reconstructs the original data from the compressed representation. By training the autoencoder on a large dataset of fluid mechanics data, the network can learn to identify the most important patterns in the data.

Once the autoencoder is trained, it can be used to detect patterns in new fluid mechanics datasets. By feeding new data through the encoder, the network can compress the data into a low-dimensional representation, which can then be analyzed to identify patterns in the data. This approach is particularly useful for detecting patterns in high-dimensional datasets, such as those commonly found in fluid mechanics.

Details about the application of autoencoders for patterns identification can be found in:

[*Muñoz, E., Dave, H., D’Alessio, G., Parente, A., Le Clainche, S., Extraction and analysis of flow features in planar synthetic jets using different machine learning techniques, preprint in ARXIV, 2023.*](https://www.researchgate.net/publication/370277088_Extraction_and_Analysis_of_Flow_Features_in_Planar_Synthetic_Jets_Using_Different_Machine_Learning_Techniques) 

[*Evazi, H. Le Clainche, S., Hoyas, S., Vinuesa, R., Towards extraction of orthogonal and parsimonious non-linear modes from turbulent flows, Exp. Syst. Appl., 202, 117038, 2022.*](https://www.sciencedirect.com/science/article/pii/S0957417422004535)

The following video explains how this neural network works:

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/Autoencoders_Video.mp4?raw=true" type="video/mp4">
</video>

### Reconstruction
Hybrid predictive reduced order models have been developed combining modal decomposition techniques and deep learning architectures. Modal decompositions reduc e data dimensionaliy and identifying the main patterns describing the physics of the dynamical system. Then, neural networks are used to predict the evolution in time the dimensionality reduced dataset. ModelFLOWs-app presents an algorithm combining singular value decomposition with convolutional or recurrent neural networks. 

Singular Value Decomposition (SVD) is a matrix decomposition technique that can be used to identify the most important patterns in a fluid mechanics dataset. When the dataset is downsampled or compressed, some of the important patterns may be lost. To reconstruct the original dataset, SVD can be used to decompose the downsampled data into three matrices: U, S, and V. These matrices contain the left singular vectors, singular values, and right singular vectors, respectively. A neural network (NN) is then trained using these three matrices as inputs to reconstruct the original dataset. The neural network learns to generate predictions of the missing values in the downsampled dataset based on the patterns identified by SVD. By combining the predictions with the known values from the downsampled dataset, the original dataset can be reconstructed.

This application combining SVD + NNs uses data from sensors or under-resolved data and reconstruct the dataset. More details can be found in:

[*Díaz, P., Corrochano, A., López-Martín, M., Le Clainche, S., Deep Learning combined with singular value decomposition to reconstruct databases in fluid dynamics, arXiv:2305.08832, 2023.*](https://arxiv.org/abs/2305.08832)

The following video explains how this hybrid predictive reduced order models works for data reconstruction:

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/DL%20superresolution.mp4?raw=true" type="video/mp4">
</video>

### Prediction
Hybrid predictive reduced order models have been developed combining modal decomposition (singular value decomposition, SVD) and deep learning architectures (neural networks, NNs). Modal decompositions reduce data dimensionaliy and identifying the main patterns describing the physics of the dynamical system. Then, neural networks are used to predict the evolution in time the dimensionality reduced dataset. ModelFLOWs-app presents an algorithm combining singular value decomposition with convolutional or recurrent neural networks (CNN or RNN). Additionally, a full deep learning model for fluid mechanics predictions is presented. This model consist of multiple layers of neural networks, such as RNN and CNN. 

In this application, the hybrid reduce order model, or full deep learning model (directly feeding the NN) is deveoped for temporal forecasting. For such aim, the input data is first preprocessed, which  includes normalization and scaling of the database.

In the full deep learning model, the preprocessed data is then fed into the NN, which learns to identify complex patterns in the fluid mechanics data and make predictions based on those patterns. The output of the NN can be a single value or a vector of values, depending on the specific prediction task.

In the hybrid reduced order model the preprocessed data is then fed into the SVD first and next into the NN. In this approach, the original dataset is first decomposed using SVD into three matrices - U, S, and V. The U and V matrices contain the left and right singular vectors, respectively, which capture the most important patterns in the data. The S matrix contains the singular values, which represent the relative importance of each pattern. These matrices are then used as input to a neural network, which can consist of RNN (in particular LSTM) and 1D CNN layers, among others. This approach allows the neural network to learn from the most important patterns in the data, identified by SVD, and to make predictions based on those patterns. The output of the neural network can also be a single value or a vector of values, depending on the specific prediction task.

Both approaches have their advantages and disadvantages, and the choice of approach depends on the specific problem and available data. A full deep learning model can be more flexible and can potentially capture more complex patterns in the data. However, it requires a large amount of data and computing resources for training. On the other hand, a hybrid deep learning model that utilizes SVD before training can be more efficient and can work well with smaller datasets. However, it may not capture all the complex patterns in the data, as it is limited to the patterns identified by SVD.

More details about the main algorithm and some of their applications can be found in:

[*Abadía-Heredia, R., Lopez-Martin, M., Carro, B., Arribas, J.I., Pérez, J.M., Le Clainche, S., A predictive hybrid reduced order model based on proper orthogonal decomposition combined with deep learning architectures, Exp. Syst. Appl., 187, 115910, 2022.*](https://www.sciencedirect.com/science/article/pii/S0957417421012653)  

[*Corrochano, A., Freitas, R.S.M., Parente, A., Le Clainche, S., A predictive physics-aware hybrid reduced order model for reacting flows, arXiv:2301.09860, 2023.*](https://arxiv.org/abs/2301.09860)

[*Mata, L., Abadía-Heredia, R., López-Martín, M., Pérez, J.M., Le Clainche, S., Forecasting through deep learning and modal decomposition in multi-phase concentric jets, arXiv:2212.12731, 2022.*](https://arxiv.org/abs/2212.12731)

The following videos explain how this hybrid predictive reduced order models works for temporal forecasting:

**Full Deep Learning**

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/Full_DL_RNN_CNN.mp4?raw=true" type="video/mp4">
</video>
<iframe width="560" height="315" src="https://www.youtube.com/embed/ldSkguBpomY?si=NxMGArajpA_i33P0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

**Hybrid Deep Learning**

<video width="640" height="360" controls>
  <source src="https://github.com/modelflows/modelflowsapp/blob/master/assets/vid/HybridDL_Video.mp4?raw=true" type="video/mp4">
</video>
