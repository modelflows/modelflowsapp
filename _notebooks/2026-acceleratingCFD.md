---
layout: post
title: "AI-Accelerated CFD"
topic: "Hybrid AI-CFD"
tldr: "Accelerate computational fluid dynamics simulations using hybrid POD–Deep Learning reduced-order models."
order: 4
---

Modern engineering flows are governed by complex, high-dimensional dynamics that standard CFD solvers resolve at significant computational cost. Parametric studies, design optimisation loops, and long unsteady simulations can easily demand thousands of CPU hours — making rapid exploration or real-time prediction practically out of reach. The tools and methodologies presented here address this challenge directly: by exploiting the low-dimensional structure inherent to most engineering flows, they enable fast, reliable predictions that complement or accelerate full CFD runs, opening the door to workflows that would otherwise be computationally prohibitive.


1. [Accelerate unsteady solutions](#accelerate-unsteady)

2. [ROMIA: A methodology to accelerate RANS](#romia)


## Accelerate unsteady solutions <a id="accelerate-unsteady"></a>

Long-horizon prediction of unsteady flows remains a major challenge in computational fluid dynamics (CFD). Full CFD simulations are accurate, but they are expensive when many time steps, operating conditions, or design iterations are required. Data-driven reduced-order models can strongly accelerate prediction, but their autoregressive errors may gradually accumulate, especially when the forecast horizon is long or when the flow regime changes.

A step-by-step tutorial describing the full workflow is available here. <a href="{{ '/software/tutorials/2026-accelerateCFD-tutorial/' | relative_url }}">Accelerate unsteady solutions</a>


## ROMIA: A methodology to accelerate RANS <a id="romia"></a>

RANS simulations of urban or industrial flows on meshes of several million cells can require thousands of iterations to converge, with computation times of hours to days even on parallel clusters. A large fraction of this cost is concentrated in the final convergence stage, where the dominant flow structure is already established and the solver is simply relaxing towards the steady-state attractor. This work presents ROMIA (Reduced Order Model for Industrial Acceleration), a non-intrusive modal prediction pipeline that learns a reduced-order model of the flow dynamics from intermediate simulation snapshots, extrapolates the asymptotic state, and reinjects it into the solver as an initial condition — bypassing the computationally expensive tail of the simulation.

A step-by-step tutorial showing how to use ROMIA from snapshot extraction to modal reconstruction and error analysis is available here. <a href="{{ '/software/tutorials/romia-user-guide/' | relative_url }}"ROMIA user guide</a>>

