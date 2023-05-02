---
layout: page
title: Tutorials
subtitle: How does the app work?
---

This data-driven application consists of two modules: **Modal Decomposition** and **Deep Learning**. Both blocks consist of algorithms capable of **detecting patterns**, **reconstructing** and **predicting data** from complex flow databases.

## Modal Decomposition
### Pattern detection
#### HODMD
HODMD, or Higher Order Dynamic Mode Decomposition, is a mathematical technique used to analyze complex dynamical systems. It has gained attention in the fluid mechanics community as a powerful tool for pattern detection. HODMD enables the decomposition of high-dimensional data into a set of dynamic modes that represent spatiotemporal patterns in the data. These dynamic modes are computed by solving an optimization problem, which identifies the most relevant temporal and spatial patterns in the data. Once the dynamic modes have been computed, they can be used to perform a variety of analyses, including mode stability analysis, mode mixing analysis, and prediction of future behavior. By applying HODMD to flow data, researchers can identify patterns related to vortex shedding, boundary layer separation, and other important fluid flow phenomena.

HODMD is also applicable to other complex dynamical systems such as chemical reactions, biological processes, and weather patterns. Its ability to extract dynamic modes from high-dimensional datasets makes it a valuable tool for analyzing complex systems that are difficult to understand using traditional analysis techniques. The use of HODMD in combination with other methods, such as machine learning algorithms, can enhance the accuracy and predictive power of the analysis. As such, HODMD is an exciting and promising technique for pattern detection and analysis in a variety of fields, including fluid mechanics.

The following videos explain how this algorithm is applied using a classic and iterative approach:

--VIDEOS GO HERE--

#### HOSVD
HOSVD, or Higher-Order Singular Value Decomposition, is a mathematical technique used in pattern detection and analysis for high-dimensional data. HOSVD can be used to decompose a high-dimensional tensor into a set of orthogonal rank-1 tensors, which represent the underlying patterns in the data. The technique allows for the extraction of features that are relevant for further analysis, such as the spatiotemporal behavior of a system.

HOSVD has been used in various fields, including image and signal processing, and has gained attention in fluid mechanics for pattern detection. By applying HOSVD to flow data, researchers can identify patterns related to vortices, turbulence, and other important fluid flow phenomena. HOSVD can also be used in combination with other techniques, such as machine learning algorithms, to enhance the accuracy and predictive power of the analysis.

The following video explains how this algorithm is applied:

--VIDEO GOES HERE--

### Reconstruction
#### Gappy data reconstruction and gappy data enhancement
Gappy data reconstruction and gappy data enhancement are two different techniques used to address different aspects of missing or incomplete data.

Gappy data reconstruction is a technique used to fill in missing or incomplete data points in a dataset, using various methods such as linear regression, interpolation, and extrapolation. The goal is to reconstruct a complete dataset that can be analyzed using traditional analysis techniques.

On the other hand, gappy data enhancement is a technique used to improve the quality of a dataset that contains incomplete or noisy data. This technique involves using statistical methods to identify and remove noise from the data, or to fill in missing data points with more accurate estimates. The goal is to produce a more accurate and reliable dataset that can be used for further analysis.

Both techniques are useful for dealing with incomplete or noisy data, but they address different aspects of the problem. Gappy data reconstruction aims to fill in missing data points, while gappy data enhancement aims to improve the overall quality of the dataset.

The following video explains how this technique is applied:

--VIDEO GOES HERE--

### Prediction
#### HODMD
In fluid mechanics, predicting the behavior of complex flow systems is crucial for optimizing system performance and improving safety. Higher Order Dynamic Mode Decomposition (HODMD) is a powerful tool that can be used to make predictions about the future behavior of fluid flow systems based on past data. By identifying the most relevant spatiotemporal patterns in the flow data using HODMD, researchers can use these patterns to make accurate predictions about the future behavior of the system.

For example, HODMD can be used to identify the spatiotemporal patterns associated with vortices or turbulence in fluid flow. These patterns can then be used to predict the future behavior of the system, such as the development of vortices or turbulence at different times and locations. This information can be used to optimize system design, reduce energy consumption, and improve safety in a variety of fluid flow applications, such as aircraft design, combustion systems, and weather forecasting.

The following videos explain how this algorithm is applied using a classic and iterative approach:

--VIDEOS GO HERE--

## Deep Learning
### Pattern detection
Autoencoders are a powerful tool for pattern detection in fluid mechanics datasets using deep learning. An autoencoder is a neural network architecture that consists of an encoder and a decoder. The encoder compresses the input data into a low-dimensional representation, while the decoder reconstructs the original data from the compressed representation. By training the autoencoder on a large dataset of fluid mechanics data, the network can learn to identify the most important patterns in the data.

Once the autoencoder is trained, it can be used to detect patterns in new fluid mechanics datasets. By feeding new data through the encoder, the network can compress the data into a low-dimensional representation, which can then be analyzed to identify patterns in the data. This approach is particularly useful for detecting patterns in high-dimensional datasets, such as those commonly found in fluid mechanics.

The following video explains how this neural network works:

--VIDEO GOES HERE--

### Reconstruction
Singular Value Decomposition (SVD) is a matrix decomposition technique that can be used to identify the most important patterns in a fluid mechanics dataset. When the dataset is downsampled or compressed, some of the important patterns may be lost. To reconstruct the original dataset, SVD can be used to decompose the downsampled data into three matrices: U, S, and V. These matrices contain the left singular vectors, singular values, and right singular vectors, respectively.

A neural network is then trained using these three matrices as inputs to reconstruct the original dataset. The neural network learns to generate predictions of the missing values in the downsampled dataset based on the patterns identified by SVD. By combining the predictions with the known values from the downsampled dataset, the original dataset can be reconstructed.

The following video explains how this neural network works:

--VIDEO GOES HERE--

### Prediction
A full deep learning model for fluid mechanics predictions can consist of multiple layers of neural networks, such as LSTM and 1D CNN. The input data is first preprocessed, which can include normalization and feature scaling. The preprocessed data is then fed into the neural network, which learns to identify complex patterns in the fluid mechanics data and make predictions based on those patterns. The output of the neural network can be a single value or a vector of values, depending on the specific prediction task.

On the other hand, a hybrid deep learning model that utilizes SVD before training can also be used for fluid mechanics predictions. In this approach, the original dataset is first decomposed using SVD into three matrices - U, S, and V. The U and V matrices contain the left and right singular vectors, respectively, which capture the most important patterns in the data. The S matrix contains the singular values, which represent the relative importance of each pattern. These matrices are then used as input to a neural network, which can consist of LSTM and 1D CNN layers, among others. This approach allows the neural network to learn from the most important patterns in the data, identified by SVD, and to make predictions based on those patterns. The output of the neural network can also be a single value or a vector of values, depending on the specific prediction task.

Both approaches have their advantages and disadvantages, and the choice of approach depends on the specific problem and available data. A full deep learning model can be more flexible and can potentially capture more complex patterns in the data. However, it requires a large amount of data and computing resources for training. On the other hand, a hybrid deep learning model that utilizes SVD before training can be more efficient and can work well with smaller datasets. However, it may not capture all the complex patterns in the data, as it is limited to the patterns identified by SVD.

The following videos explain how these neural networks work:

--VIDEOS GO HERE--
