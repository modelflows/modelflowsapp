---
layout: page
category: "Adaptive Methodologies"
topic: "RANS acceleration"
tldr: "A divergence-aware adaptive CFD-surrogate framework that alternates between fast POD-DL forecasting and targeted OpenFOAM recalls for robust long-horizon prediction of unsteady flows."
title: "ROMIA: A methodology to accelerate RANS"
author: "Ángel Alonso, Miguel Rios"
---


# Modal Prediction Pipeline for Accelerating Urban Flow CFD Simulations

RANS simulations of urban or industrial flows on meshes of several million cells can require thousands of iterations to converge, with computation times of hours to days even on parallel clusters. A large fraction of this cost is concentrated in the final convergence stage, where the dominant flow structure is already established and the solver is simply relaxing towards the steady-state attractor. This work presents **ROMIA (Reduced Order Model for Industrial Acceleration)**, a non-intrusive modal prediction pipeline that learns a reduced-order model of the flow dynamics from intermediate simulation snapshots, extrapolates the asymptotic state, and reinjects it into the solver as an initial condition — bypassing the computationally expensive tail of the simulation.

The pipeline is developed by the [ModelFlows group](https://modelflows.github.io/modelflowsapp/) at Universidad Politécnica de Madrid. This study constitutes the **first validation of ROMIA**, proving the value of the approximation on industrial and urban cases.

---

# Methodology

## Pipeline Overview

ROMIA operates as a non-intrusive layer on top of OpenFOAM, requiring no modification of the solver. It chains four sequential stages during a running simulation:

<!-- IMAGES -->
<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/b679d419508eb645aedfe728bebb6c5a1937c62e/assets/img/post_ROMIA_research/flujoromia.png?raw=true" alt="ROMIA pipeline" width="60%">
</p>
*Figure 1. Schematic of the ROMIA pipeline. Snapshots captured during the transient phase are compressed spatially by iPOD, modelled temporally by HODMD, and the predicted asymptotic state is reconstructed and reinjected into the solver when the trigger criterion is satisfied.*

## Spatial Reduction: Incremental POD (iPOD)

At each snapshot interval, the current flow field, that lives in a space of dimensions N on the orders of tens of millions of parameters, is projected onto a low-dimensional basis maintained by Incremental Proper Orthogonal Decomposition (iPOD). The basis is updated online as new snapshots arrive, without recomputing the full SVD from scratch. The number of retained modes is controlled by an energy threshold ε₁, defined as the fraction of modal energy discarded relative to the total. This reduces the high-dimensional state to a compact set of temporal coefficients a(t) ∈ ℝʳ, where r ≪ N.

## Temporal Modelling: HODMD

Higher-Order Dynamic Mode Decomposition (HODMD) is applied to the series of reduced coefficients a(t). By constructing augmented snapshot matrices with a time-delay parameter d, HODMD identifies the spectral content of the dynamics even when the number of physically distinct frequencies exceeds the spatial rank of the reduced basis. Each extracted mode carries a growth rate δₘ and a frequency ωₘ.

For stationary attractors, only modes with growth rate close to zero (|λⱼ| − 1 ≤ ε_δ) and frequency close to zero (|ℑ(ωⱼ)| ≤ ε_φ) are retained. The asymptotic state is predicted as the superposition of these stationary modes:

**a**_∞ = Re( Σⱼ∈S ψⱼ bⱼ )

where S denotes the set of stationary modes, ψⱼ are the modal shapes and bⱼ their amplitudes.

## Automatic Trigger

The pipeline monitors prediction quality in real time through three criteria: spectral stability of the identified stationary modes, one-step prediction error against observed coefficients, and temporal stability of **a**_∞ between successive evaluations. When all criteria are simultaneously satisfied, the trigger authorises the jump: the simulation is stopped, the full physical field is reconstructed via

**x**_pred = **x̄** + Φ **a**_∞

and reinjected into OpenFOAM as a restart condition. The solver then runs a short validation phase to confirm convergence. If the prediction is rejected, the simulation continues normally, so a failed prediction never corrupts the final result.

---

# Validation Case I — Urban Flow

## Geometry and Flow Conditions

This validation case reproduces **AIJ Case C**, a canonical wind-tunnel benchmark of the Architectural Institute of Japan, consisting of a 3×3 array of nine square-section buildings of height H = 0.2 m with equal spacing H between them. The Reynolds number, based on the inflow velocity at building height U_H = 3.654 m/s and kinematic viscosity ν = 1.5 × 10⁻⁵ m²/s, is Re ≈ 4.9 × 10⁴.


<!-- IMAGES -->
<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/b679d419508eb645aedfe728bebb6c5a1937c62e/assets/img/post_ROMIA_research/GeometriaCaso.png?raw=true" alt="Geometry of the case" width="60%">
</p>



## Computational Setup

The CFD simulation was performed in **OpenFOAM v12** using the *simpleFoam* steady-state solver with a **RANS k–ε turbulence model**. The computational mesh is an unstructured polyhedral grid of **3,666,741 cells**, selected after a three-level convergence study (coarse / medium / fine) with two progressive refinement boxes around the building array. Boundary conditions include a stratified Dirichlet inlet profile reproducing the atmospheric boundary layer (ABL), no-slip conditions on all solid surfaces, and a zero-pressure outlet.

---

# Parameter Sensitivity and Automatic Calibration

ROMIA depends on five parameters that govern the different stages of the pipeline (ε₁, d, w, ε_δ, ε_φ). A key feature of the methodology is its ability to calibrate these parameters automatically during the simulation, without prior knowledge of the converged solution. To verify this capability and identify the operating ranges suitable for urban RANS flows, a systematic sensitivity analysis was conducted on the AIJ Case C configuration.

Another key feature of ROMIA is its ability to trigger the reconstruction at the optimal moment, minimising the reconstruction error. This analysis also detects, with offline and previously simulated data, the optimal moment to trigger.

## Sensitivity Analysis

The following figures show the reconstruction error as a function of each parameter, with the remaining parameters held fixed at their baseline values.


<!-- IMAGES -->
<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/b679d419508eb645aedfe728bebb6c5a1937c62e/assets/img/post_ROMIA_research/02_sensibilidad_epsilons.png?raw=true" alt="" width="60%">
</p>
*Figure 2. Sensitivity to the spatial energy threshold ε₁.*

<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/b679d419508eb645aedfe728bebb6c5a1937c62e/assets/img/post_ROMIA_research/06_sensibilidad_global_d.png?raw=true" alt="" width="60%">
</p>
*Figure 3. Sensitivity to the HODMD time-delay parameter d.*

<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/e8f9f91e92b9a73ddb30eb2fcc3c26458171c327/assets/img/post_ROMIA_research/01_pareto_front.png?raw=true" alt="" width="60%">
</p>
*Figure 4. Relation between number of POD modes, snapshot of trigger, and reconstruction error.*

<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/e8f9f91e92b9a73ddb30eb2fcc3c26458171c327/assets/img/post_ROMIA_research/07_tradeoff_cuantitativo_Uy.png?raw=true" alt="" width="60%">
</p>
![best snapshot](07_tradeoff_cuantitativo_Uy.png)
*Figure 5. Optimal moment to trigger the reconstruction as a function of iteration number.*


The analysis of sensitivity shows that the best moment to trigger the prediction is around iteration 1250. The optimal number of retained modes lies between 10 and 15, with an optimal spatial energy threshold ε₁ = 10⁻⁴ and modal amplitude threshold ε₂ = 5 × 10⁻⁴.

## Automatic Calibration Results

The sensitivity analysis identifies the ranges within which accurate reconstruction is achievable. ROMIA's automatic calibration procedure, operating without access to the reference solution, selected the following parameters:

| Parameter | Manual optimum | ROMIA selection |
|-----------|---------------|-----------------|
| Trigger iteration | 1250 | 1350 |
| d | 15 | 20 |

The automatically selected values fall within the acceptable ranges identified by the sensitivity analysis, confirming that the calibration procedure generalises correctly to this flow regime.

# Results — Urban Flow

## Low-Dimensionality of the Flow

The singular value spectrum of the iPOD basis confirms the low-dimensionality hypothesis underlying the ROM approach. With **r = 10 modes**, the pipeline retains **99.99% of the modal energy** of a state space of approximately 15 million parameters. This result demonstrates that, despite the geometric complexity of nine interacting bluff bodies, the transient evolution of the flow inhabits a subspace of very low dimension, validating the applicability of the ROM framework to this flow regime.

## Prediction Accuracy

The pipeline triggered at **iteration 1350** and predicted the converged state corresponding to **iteration 4000**, saving approximately **2200 solver iterations** and achieving a **speed-up of 2.2×** relative to the full simulation.

Following the prediction of the converged state, ROMIA restarted the solver and ran 200 additional CFD iterations to validate the physical consistency of the reconstructed field and refine the solution.

The figures below compare the ROMIA prediction against the CFD reference field on a horizontal slice at building height:


<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/4ff5ea0e5456a35b771713d8d90c8104eb70c186/assets/img/post_ROMIA_research/urban-romia-comparison.png?raw=true" alt="" width="60%">
</p>
*Figure 6. Comparasion between the reconstruction on Uy, p and the ground truth*.


Quantitative reconstruction errors are reported in the table below:

| Field | L² relative error |
|-------|------------------|
| U_y (main flow direction) | ~3% |
| U_x (lateral) | ~15% |
| U_z (vertical) | ~15% |
| p (pressure) | ~15% |

The dominant velocity component U_y is reconstructed with ~3% L² error. The higher relative errors in U_x, U_z and p are partly a metric artefact: these fields are nearly zero across most of the domain, concentrated in the inter-building recirculation zones, so small absolute errors in those regions produce disproportionately large relative values. Visual inspection of the field comparisons confirms that the spatial structure of all fields is correctly reproduced.

---

# Validation Case II — Formula 1 Rear Wing

The second validation case extends ROMIA to a fully industrial geometry: the rear wing of a Formula 1 single-seater, discretised on a mesh of **29,482,757 cells** — an order of magnitude larger than the urban case. The objective is to demonstrate that the pipeline scales to production-level HPC workloads and that the automatic calibration generalises across geometrically distinct flow regimes.

## Geometry and Flow Conditions

The computational domain includes the rear wing profile, its immediate wake, and the surrounding control volume. The inflow is horizontal with uniform velocity U∞ = 73 m/s, giving a Reynolds number of Re ≈ 3.5 × 10⁶ based on the mean wing chord.


<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/c8dee9bb0198d63f18693a920031baff3356eb7b/assets/img/post_ROMIA_research/Contorno1_aleron.png?raw=true" alt="" width="60%">
</p>
*Figure 7. Validation case: Formula 1 rear wing. Horizontal inflow at U∞ = 73 m/s.*



## Computational Setup

The CFD simulation was performed in **OpenFOAM 2506** using the *simpleFoam* steady-state solver with a **standard k–ε turbulence model**, executed in parallel on **72 processors**. ROMIA operated in managed mode with **10% spatial subsampling** (cell_volume_sqrt strategy), resulting in 3,537,930 subsampled cells. The pipeline was configured with a warmup phase of 100 iterations, followed by snapshot accumulation at writeInterval = 2 from iteration 102 onwards, producing 200 snapshots in batches of 5.

## Results — Formula 1 Rear Wing

### Low-Dimensionality of the Transient Flow

The singular value spectrum exhibits a pronounced spectral separation: the first mode concentrates σ₁ = 4881.5, while σ₂ = 402.9 and σ₃ = 131.7. The ratio σ₁/σ₈₀ ≈ 5.77 × 10⁴ demonstrates extreme energy concentration in the leading modes, characteristic of external flows over aerodynamic bodies where a global displacement mode dominates the convergence trajectory.

| Modes retained (r) | Cumulative modal energy |
|--------------------|------------------------|
| 2 | 99.85% |
| 5 | 99.989% |
| 10 | 99.999% |

With only **5 POD modes on 10% of the cells**, ROMIA retains 99.989% of the modal energy from a state space of approximately 2.1 × 10⁷ degrees of freedom in the subsample. The spatial compression ratio is of the order N/r ≈ 2.6 × 10⁵. The iPOD basis stabilised operationally at **r = 80 modes** after approximately 80 snapshots (iteration ≈ 260).

### Asymptotic State Identification

The HODMD autocalibration procedure autonomously selected the optimal configuration **(d = 20, window = 180)**, operating over r = 80 POD modes. The fit extracted **4 dynamic modes**, all classified as stationary:

| Mode | \|λ\| | Growth rate σ (iter⁻¹) | Frequency ω (rad/iter) |
|------|--------|------------------------|------------------------|
| 1 | 1.027 | 1.31 × 10⁻² | +5.29 × 10⁻³ |
| 2 | 1.027 | 1.31 × 10⁻² | −5.29 × 10⁻³ |
| 3 | 1.021 | 1.06 × 10⁻² | +1.50 × 10⁻² |
| 4 | 1.021 | 1.06 × 10⁻² | −1.50 × 10⁻² |

No unstable or damped modes were detected. The oscillation frequencies (ω ∼ 10⁻²–10⁻³ rad/iteration) are compatible with quasi-stationary convergence towards the solver fixed point.

### Field Reconstruction and Computational Speed-Up

The trigger declared **READY at iteration 500**. Following reconstruction and restart, all residuals decay monotonically over 200 additional iterations, with no blow-up or numerical oscillations. The maximum residual at iteration 10200 was 1.06 × 10⁻⁴, comparable to the convergence level reached prior to restart.

<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/75680a61c27e9a8f6dede6c98d5d28849f49f76c/assets/img/post_ROMIA_research/Contour_Umag_Romia_vs_CFD.png?raw=true" alt="" width="60%">
</p>
*Figure 8. Velocity magnitude |U| Left: ROMIA reconstructed field (iter. 10000). Right: Ground truth.*

<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/2ddad4d1563df822bcbd402ccf8066ca932be23c/assets/img/post_ROMIA_research/Contour_ps_Romia_vs_CFD.png?raw=true" alt="" width="60%">
</p>
*Figure 9: Presion field Left: ROMIA reconstructed field (iter. 10000). Right: Ground truth.*

<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/2ddad4d1563df822bcbd402ccf8066ca932be23c/assets/img/post_ROMIA_research/L2_abs_percent_U_mag.png?raw=true" alt="" width="60%">
</p>
*Figure 10. L2 Error of U field*


<p style="text-align: center;">
<img src="https://github.com/modelflows/modelflowsapp/blob/2ddad4d1563df822bcbd402ccf8066ca932be23c/assets/img/post_ROMIA_research/L2_abs_percent_p.png?raw=true" alt="" width="60%">
</p>
*Figure 11. L2 Error of presion field* 

The pipeline was evaluated against a baseline run without ROM intervention:

| Configuration | Wall-clock time |
|---------------|----------------|
| Baseline (full simpleFoam) | 15 h 54 m |
| ROMIA (warmup + iPOD + trigger + restart) | 6 h 32 m |
| **Speed-up** | **2.49×** |

ROMIA reduced the wall-clock time by a factor of approximately **2.5×**, saving roughly 60% of the total computation time on a 29.5-million-cell industrial mesh running on 72 parallel processors.

---

# Summary

The ROMIA pipeline has been validated on two geometrically distinct RANS flow regimes, demonstrating consistent behaviour across both cases:

| | Urban flow (AIJ Case C) | F1 rear wing |
|---|---|---|
| Mesh size | 3.6 M cells | 29.5 M cells |
| POD modes (99.99% energy) | 10 | 5 |
| Trigger iteration | 1350 | 500 |
| Speed-up | 2.2× | 2.5× |
| L² error (dominant field) | ~3% (U_y) | — |

Key findings across both cases:

- The transient RANS dynamics inhabit a subspace of very low dimension relative to the full state space, confirming the low-dimensionality hypothesis in both flow regimes.
- HODMD autocalibration autonomously identifies the optimal time-delay and window parameters without manual intervention.
- The multi-layer trigger avoids premature reconstruction, waiting for sufficient snapshot accumulation and autocalibration validation before declaring READY.
- The reconstructed fields are accepted by the OpenFOAM solver without divergence, and residuals converge monotonically after restart in both cases.

---

