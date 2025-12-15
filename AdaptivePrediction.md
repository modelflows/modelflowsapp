---
layout: page
title: Adaptive prediction
subtitle: Our studies focused on adaptive prediction
---

## Introduction
While high-fidelity numerical simulations are indispensable for accurate prediction through the resolution of all relevant spatiotemporal scales, their prohibitive computational cost often renders them impractical for iterative tasks such as parameter optimization and high-throughput studies. To alleviate this limitation, surrogate modeling has emerged as a powerful alternative, particularly through the synergistic integration of Proper Orthogonal Decomposition (POD) and Deep Learning (DL). POD efficiently reduces dimensionality by extracting dominant energetic modes, while DL captures strongly nonlinear temporal dynamics and implicit energy transfer mechanisms. Nevertheless, a critical challenge persists in controlling prediction divergence, whereby data-driven models progressively drift from their training manifold, leading to error accumulation or even catastrophic failure for long-term predictions. Adaptive prediction strategies are therefore essential to maintain robust long-term accuracy under evolving flow regimes or previously unseen conditions, thereby enabling Reduced-Order Models (ROMs) to evolve from purely offline approximations into reliable online predictors suitable for real-time optimization and closed-loop control.


## Framework of adaptive prediction
An adaptive prediction framework for fluid dynamics was developed by coupling OpenFOAM with a POD-DL solver. To reduce computational cost while preserving high accuracy over long-time simulations, OpenFOAM and the POD-DL model operate in an alternating manner. The prediction horizon of the POD-DL model is determined using three complementary strategies: (i) prediction over a prescribed fixed time interval; (ii) online evaluation of consistency and truncation error estimates during prediction, with OpenFOAM dynamically re-invoked when predefined thresholds are exceeded; and (iii) real-time computation of the Mahalanobis distance and ensemble-based uncertainty quantification, which automatically triggers a recall of OpenFOAM when model confidence degrades. The entire coupling and control process is orchestrated via Linux shell scripts. The proposed framework and associated algorithms are validated using the canonical flow around a circular cylinder.

<!-- IMAGES -->
![Figure text](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/Adaptive_framework.png?raw=true)
