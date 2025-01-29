---
layout: page
title: Notebooks: Modal Decomposition
<!--subtitle: GENERAL SUBTITLE -->
---

<!-- Comment -->

Codes available:
* [Higher-Order Singular Value Decomposition (HOSVD)](https://modelflows.github.io/modelflowsapp/modaldecomposition/#hosvd)
* [Higher-Order Dynamic Mode Decomposition (HODMD)](https://modelflows.github.io/modelflowsapp/modaldecomposition/#hodmd)

## HOSVD
The Higher-Order Singular Value Decomposition (HOSVD) is a generalization of the standard SVD to tensors, 
enabling the decomposition of multi-dimensional data into a core tensor and orthonormal factor matrices along each mode.
This method is widely used in modal decomposition, data compression, and feature extraction, particularly in fields dealing with high-dimensional datasets such as fluid dynamics and biomedical imaging. 
By capturing dominant structures in data, HOSVD facilitates reduced-order modeling and pattern recognition while preserving key spatial and temporal correlations.


## HODMD
The Higher-Order Dynamic Mode Decomposition (HODMD) extends the traditional DMD to handle high-dimensional and multiway data efficiently by leveraging tensor decomposition techniques. 
By applying HOSVD as a preprocessing step, HODMD reduces noise sensitivity and improves the extraction of dominant spatiotemporal modes in complex dynamical systems. 
This makes it particularly useful for analyzing fluid flows, biomedical signals, and other time-dependent datasets, enabling reduced-order modeling and predictive analysis while maintaining the underlying system dynamics.

