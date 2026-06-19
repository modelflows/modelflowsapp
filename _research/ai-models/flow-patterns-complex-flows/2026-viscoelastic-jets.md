---
layout: post
title: "Reduced-order modeling of viscoelastic flows"
category: "AI & Data-Driven Models"
topic: "Flow Patterns in Complex Flows"
thumbnail: "/assets/img/flow-patterns-complex-flows/thumbnail_viscoelastic-jet.png"
tldr: "Modal decompositions for studying and modeling viscoelastic turbulent planar jets"
---

Newtonian fluids, like air and water, follow Newton's Law of Viscosity, which states that the shear stress is directly proportional to the velocity gradient. The constant of proportionality is commonly known as the dynamic viscosity of the fluid. On the contrary, non-Newtonian fluids do not follow this law. This is the case of mayonnaise, topical creams or paints, which showcase more complex behaviors such as fluid elasticity, yield-stress or shear-dependent viscosity. 

In this post, we focus on polymeric solutions that have viscous and elastic properties, or viscoelastic flows. In turbulent flows, polymers draw kinetic energy, they turn into elastic energy by polymer stretching, and either return to the flow or dissipate. This mechanism can change drastically the flow, and it translates into macroscopic effects such as drag reduction, enhanced heat transfer, and elastic instabilities.

These effects are commonly studied through experiments and numerical simulations. Numerical simulations provide a complete characterization of the flow and the polymer dynamics. However, the hyperbolic nature of the polymer equation supposes a great challenge, where numerical instabilities appear as polymer elasticity increases. To solve this issue, numerical solvers implement sophisticated methods, that in turn increase significantly the cost of numerical simulations.

Here, we propose reduced-order models for accelerating numerical simulations. We split this contribution in two parts:

1. **Dimensionality reduction through modal decompositions**
We demonstrate that the complex dynamics can be interpreted as a superposition of a few coherent structures.

2. **Reduced-order modeling with hybrid machine learning**
We describe a surrogate model that combines modal decompositions with a deep neural network for temporal forecasting. 

---

## Coherent structures
We first show the application of modal decompositions for identifying the dominant coherent structures in the viscoelastic turbulent planar jet. 

Modal decompositions decompose the data into a superposition of modes, each accompanied by characteristic values that represent either their energy content or dynamical traits. Modal decompositions require large datasets, and they can be used, for example, for [reconstructing flow fields from sparse measurements](https://modelflows.github.io/modelflowsapp/research/2026-from-sensors-to-3d-reconstruction/). Here, we use modal decompositions for compressing high-dimensional data into a more interpretable low-dimensional form by means of the higher order dynamic mode decomposition (HODMD); more information about the method and applications is available [here](https://modelflows.github.io/modelflowsapp/software/notebooks/2026-modaldecomposition/).

HODMD yields a decomposition based on DMD modes, each associated to a frequency and temporal growth/decay rate; the weighted superposition of these modes reconstructs the original data based on their most dominant coherent dynamics. The method can be tuned to consider small-amplitude dynamics, though it must be more carefully calibrated so the reconstruction does not overfit noisy or spurious dynamics. 

<p align="center">
  <img src="{{ '/assets/img/flow-patterns-complex-flows/hodmd_robust-modes.png' | relative_url }}" alt="HODMD spectra of robust DMD modes" width="80%"/>
</p>

<p align="center">
  <em>
  HODMD spectra of robust DMD modes in the viscoelastic jet. Modes are compared with those from a Newtonian turbulent planar jet.
  </em>
</p>

We reconstruct the viscoelastic turbulent planar jet using sixteen robust modes. We also performed HODMD to a Newtonian turbulent planar jet, which yielded twenty-one robust modes. We find that the turbulent dynamics in the Newtonian jet are more complex than those from the viscoelastic jet, since it is required a larger number of DMD modes to reconstruct the flow field with similar accuracy. The DMD modes can also be represented in space, where low-frequency modes are associated with global, streamwise-coherent streaks, and high-frequency modes with localized, spanwise-coherent wave packets. Remarkably, the method is also able to reconstruct the spanwise-homogeneous or roller-like structures in the near-field of the Newtonian jet, whose shape and frequency range matches with the symmetric or varicose mode of instability. 

<p align="center">
   <img src="{{ '/assets/img/flow-patterns-complex-flows/hodmd_modes-jets.png' | relative_url }}" alt="Spatial structure of robust DMD modes" width="80%"/>
</p>
 
<p align="center">
  <em>
  Spatial structures of representative robust DMD modes in the Newtonian and viscoelastic jets. The yellow-translucent surfaces mark the average location of the jet edges.
  </em>
</p>

Since the DMD modes are space-dependent, their interpretation can be improved by applying HODMD in one of the spatial directions. By applying the decomposition in the spanwise-homogeneous direction, we now describe the dynamics as a superposition of steady and traveling waves. In doing this, we find that a potential mechanism sustaining the turbulent regime in the viscoelastic jet is given by the interaction between short streaks and wave packets located in both edges in the near-field of the jet; we did not find an equivalent mechanism in the Newtonian jet, where similar streaks are found after the potential core, and transition occurs because of the modal growth of the instability. 

<p align="center">
   <img src="{{ '/assets/img/flow-patterns-complex-flows/hodmd_near-field.png' | relative_url }}" alt="Streaks and flow instability at the near-field" width="80%"/>
</p>

<p align="center">
  <em>
  Flow structures in the near-field. The streaks modify the bulk flow, where perturbations grow along the jet edges because of the interaction of the streaks with wavepacket structures at the same location.
  </em>
</p>

In the viscoelastic jet, both near-field streaks and instability are purely elastic, since the Reynolds number is too small and turbulence is rather sustained by polymer elasticity. This finding supposes, to the authors' knowledge, the first description of a transition mechanism to elastic turbulence in viscoelastic jets. 

---

## Reduced-order modeling

We have demonstrated that coherent structures offer a compact and interpretable representation of the complex dynamics in the viscoelastic turbulent planar jet; we now show that they can also be used as a good basis for building reduced-order models in the same case.

We combine proper orthogonal decomposition (POD) with a deep neural network for forecasting future states from historic data. This is done in an autoregressive way, meaning that the model uses its own prediction to condition the next step. The model is optimized during training for finding the best solution by means of minimizing the mean-squared error between the true and predicted fields in the subspace of POD modes. In doing so, we reduce the size of the model, since POD is a non-parametric method, and the amount of training data. The optimal subspace from POD is physically-interpretable, and using it during training constitutes a method for weakly enforcing the physics underlying in the system into the machine learning model.

<p align="center">
  <img src="{{ '/assets/img/flow-patterns-complex-flows/rom_pod.png' | relative_url }}" alt="POD decomposition of the viscoelastic jet" width="80%"/>
</p>
  
 <p align="center">
   <em>
   POD decomposition of the viscoelastic jet. The reconstruction with 25 POD modes yields ~50% of energy, and ~85% with 125 POD modes.
   </em>
 </p>

We adopt the POD with deep learning, or [POD-DL](https://modelflows.github.io/modelflowsapp/software/notebooks/2026-deeplearning/), for our predictor. POD-DL first reduces the dimensionality of the data by means of POD, and it implements a deep neural network for modeling the temporal evolution of the POD coefficients. The neural network couples a long short-term memory (LSTM) network that learns the long-range temporal structure of the input, with a non-linear feed-forward network (FFN) that focuses on non-linear relations between the input and output sequences. In this study, we also explore the effect of layer depth in the prediction accuracy. To do so, we introduce the POD-DL with residual, or POD-rDL, which implements skip connections and stronger regularization for stabilizing the training of deeper neural networks. 

 <p align="center">
   <img src="{{ '/assets/img/flow-patterns-complex-flows/rom_sketch.png' | relative_url }}" alt="Sketch of the deep neural networks" width="80%"/>
 </p>
      
 <p align="center">
   <em>
   Sketch of the prediction models. The symbols N and H denote the dimensionality and T the length of the output for each layer.
   </em>
 </p>

We find that depth indeed improves the accuracy of the model, with skip connections the most efficient strategy for building deep and generalizable neural networks. In addition, the POD-rDL outperforms the POD-DL predicting more complex input spaces, which are characterized by higher-order POD modes. As layer depth increases, deep learning models are able to learn more complex temporal abstractions; this allows models to learn better the multi-scale behavior of turbulent flows. However, architectural choices matter the most if, for instance, models are trained for multi-step prediction. In this case, the choice of output layer is crucial, where the POD-DL, specifically the feed-forward network that transforms non-linearly each candidate prediction step mapped from the output from the LSTM network, shows a performance similar to the POD-rDL. 

<p align="center">
  <img src="{{ '/assets/img/flow-patterns-complex-flows/rom_error.png' | relative_url }}" alt="Cumulative predictive error" width="80%"/>
</p>
  
 <p align="center">
   <em>
   Prediction error over the temporal horizon, measured as the cumulative average of the L2 error norm to the temporal horizon of the velocity field reconstructed from POD.
   </em>
 </p>

<p align="center">
  <img src="{{ '/assets/img/flow-patterns-complex-flows/rom_pred.png' | relative_url }}" alt="Prediction from POD-DL and POD-rDL" width="80%"/>
</p>
    
<p align="center">
  <em>
  Prediction from POD-DL and POD-rDL for multi-step and higher-dimensional input space predictions, respectively.
  </em>
</p>

---

## Summary

This post shows using modal decompositions for modeling viscoelastic turbulent planar jets. First, we showed HODMD for identifying the dominant coherent structures, revealing that viscoelastic dynamics are governed by fewer modes than Newtonian turbulent planar jets, and uncovering a purely elastic near-field transition mechanism driven by the interaction of streamwise streaks and wave packets at the jet edges — to the authors' knowledge. Second, a hybrid POD and deep learning architecture (POD-DL and POD-DL with residual or POD-rDL) is introduced to forecast the temporal evolution of POD mode coefficients in an autoregressive manner, with the POD subspace serving as a physically interpretable, low-dimensional basis that implicitly encodes flow physics into the learning objective. Results show that residual connections and increased network depth improve generalization, particularly for higher-order mode dynamics, establishing this hybrid framework as an efficient and interpretable surrogate for viscoelastic turbulent planar jets, that is extensible to other non-Newtonian flows.

---

## Reference

- Amor, C., Corrochano, A., Soligo, G., Le Clainche, S., & Rosti, M. E. **Coherent structures in Newtonian and viscoelastic turbulent planar jets**. *Journal of Fluid Mechanics* 1036, A7 (2026). [Link](https://doi.org/10.1017/jfm.2026.11610).

- Amor, C., Corrochano, A., Rosti, M. E., & Le Clainche, S. **Reduced-order modeling of a viscoelastic turbulent jet with hybrid machine learning models**. *Journal of Physics: Conference Series* 3230, 012001 (2026). [Link](https://doi.org/10.1088/1742-6596/3230/1/012001)

