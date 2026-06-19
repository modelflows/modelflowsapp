---
layout: page
category: "Adaptive Methodologies"
topic: "Adaptive prediction"
thumbnail: "assets/img/Adaptive_Framework.png"
tldr: "A fast adaptive prediction method that uses a lightweight AI model, calls CFD solver and retrain the model again when the prediction becomes unreliable."
title: "Speed-up CFD using adaptive hybrid ROMs: unsteady solutions"
subtitle: "Closed-loop OpenFOAM and POD-DL coupling for long-horizon unsteady-flow prediction"
published: true
---


# Divergence-aware Adaptive CFD-Surrogate Prediction

Long-horizon prediction of unsteady flows remains a major challenge in computational fluid dynamics (CFD). Full CFD simulations are accurate, but they are expensive when many time steps, operating conditions, or design iterations are required. Data-driven reduced-order models can strongly accelerate prediction, but their autoregressive errors may gradually accumulate, especially when the forecast horizon is long or when the flow regime changes.

This work develops a **divergence-aware adaptive prediction framework** that couples an OpenFOAM-based CFD solver with a **proper orthogonal decomposition-deep learning (POD-DL)** surrogate model. 

The workflow starts with high-fidelity CFD simulation. The generated CFD snapshots are used to train a reduced-order deep learning model. After training, the surrogate model is used to predict the flow evolution much faster than full CFD. During this online prediction stage, the framework continuously monitors whether the surrogate prediction is still reliable. If the prediction remains stable, the surrogate keeps running. If divergence or loss of reliability is detected, the framework automatically recalls the CFD solver, generates new high-fidelity snapshots, updates the training database, and retrains the surrogate model.

The framework is designed for realistic online prediction scenarios, where future CFD ground truth is not available during deployment. Instead of comparing the prediction with reference data, the method monitors internal reliability indicators, especially ensemble uncertainty in the POD coefficient space.


# Research Motivation

CFD simulations play an essential role in fluid mechanics, combustion, meteorology, aerodynamics, and engineering design. However, resolving the relevant spatial and temporal scales of realistic unsteady flows often requires large computational resources.

Reduced-order models provide an efficient alternative by compressing the flow field into a low-dimensional representation and learning its temporal evolution. However, purely offline surrogates face two important limitations:

- **Long-horizon error accumulation:** small prediction errors are propagated and amplified during autoregressive forecasting.
- **Poor robustness under regime changes:** a surrogate trained under one condition may lose reliability when the flow state or boundary condition changes.

The proposed framework addresses these limitations by introducing an **adaptive CFD-surrogate loop**. The surrogate is not used blindly over the full prediction horizon. Instead, its reliability is monitored online, and CFD is recalled only when new high-fidelity information is required.


# Methodology Overview

The adaptive framework contains four main components:

1. **CFD data generation** using OpenFOAM.
2. **POD compression** of high-dimensional flow snapshots.
3. **Deep-learning temporal prediction** in the reduced POD space.
4. **Online divergence monitoring** and selective CFD recall.

## Closed-loop CFD/POD-DL workflow

The workflow starts with a short CFD simulation. The generated snapshots are used to build the initial POD basis and train a neural-network predictor. After training, the surrogate model advances the reduced state autoregressively. During this prediction stage, the monitoring module evaluates whether the forecast remains reliable.

When the scheduled update time is reached, or when prediction divergence is detected, the workflow switches back to CFD. New snapshots are generated, the POD-DL model is retrained or updated, and surrogate prediction then resumes. In this way, the framework alternates between **expensive but accurate CFD simulation** and **fast but monitored POD-DL prediction**.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_Framework.png?raw=true" alt="Adaptive CFD-POD-DL framework" width="85%">
</p>

<p style="text-align: center;"><em>Figure 1. Closed-loop adaptive framework coupling online CFD simulation and POD-DL prediction. CFD snapshots are compressed by POD, the reduced coefficients are predicted by a deep-learning model, and the monitoring module decides whether the forecast can continue or whether CFD should be recalled.</em></p>

## POD-DL surrogate model

The high-dimensional CFD snapshot matrix is first mean-centered and decomposed using singular value decomposition. The dominant POD modes provide a compact basis for the unsteady flow structures. The corresponding temporal coefficients are standardized and used as the training data for a deep-learning sequence predictor.

In the present implementation, the predictor is based on a stacked **long short-term memory (LSTM)** network followed by fully connected layers. The model takes a rolling window of past POD coefficients and predicts the next coefficient block. During long-horizon forecasting, the predicted coefficients are fed back into the input window, forming an autoregressive prediction loop.

The predicted POD coefficients are finally transformed back to the physical space through inverse POD reconstruction.

## Divergence detection and adaptive control

Two adaptive strategies are considered.

### Scheduled adaptive update

In the scheduled mode, CFD is recalled after a fixed number of predicted snapshots. This is a simple and robust correction strategy. It periodically introduces new high-fidelity data and prevents irreversible growth of the prediction error.

### Event-triggered adaptive update

In the event-triggered mode, the framework recalls CFD only when the surrogate becomes unreliable. Several POD-DL predictors are trained with different random seeds and advanced simultaneously. Their disagreement is used to estimate **ensemble uncertainty** in the reduced POD space.

The uncertainty is weighted by the retained POD singular values, so uncertainty in energetically important modes contributes more strongly to the final indicator. A dynamic threshold is estimated from the recent uncertainty history using a median-MAD rule. If the uncertainty exceeds the threshold for a sustained period, the current forecast is terminated and CFD is recalled.

This event-triggered strategy is important because it does not require future CFD ground truth during prediction. The model decides when to stop based on its own reliability indicator.


# CFD Dataset Generation and Validation

The framework is assessed using the canonical problem of **three-dimensional flow past a circular cylinder**. This case is widely used for studying vortex shedding, wake instability, and unsteady-flow prediction.

## Computational setup

The CFD simulations are performed using **OpenFOAM** with the `pimpleFoam` solver for incompressible flow. The Reynolds-number range is approximately **Re = 160-400**. The computational domain has a height of 20D, an upstream length of 10D, a downstream length of 20D, and a spanwise length of 3D, where D is the cylinder diameter.

The mesh contains approximately **741 thousand cells**, with refinement near the cylinder and in the wake region. The spanwise boundaries are periodic. The inlet velocity and kinematic viscosity are adjusted to obtain different Reynolds numbers while keeping the same geometry. Probe points are placed in the wake region to evaluate the temporal evolution of velocity and pressure predicted by the surrogate.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_Geometry_Mesh.png?raw=true" alt="Computational geometry and mesh" width="90%">
</p>

<p style="text-align: center;"><em>Figure 2. Computational geometry and mesh for the circular-cylinder wake. The domain extends 10D upstream and 20D downstream of the cylinder, with a 20D cross-stream height. The mesh is refined around the cylinder and in the wake region where vortex shedding develops.</em></p>

## Numerical validation

Before training the surrogate model, the CFD setup is validated using standard integral quantities:

- mean drag coefficient,
- mean base-pressure coefficient,
- Strouhal number.

The numerical results follow the experimental trends over the investigated Reynolds-number range. The mean drag coefficient decreases gradually with Reynolds number. The base-pressure coefficient remains close to the experimental values and captures the expected tendency. The Strouhal number remains around the characteristic vortex-shedding range for cylinder wakes. This validation confirms that the generated CFD snapshots provide a reliable basis for POD-DL training and adaptive prediction.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_CFD_Validation.png?raw=true" alt="Validation of drag coefficient, base-pressure coefficient and Strouhal number" width="40%">
</p>

<p style="text-align: center;"><em>Figure 3. Validation of the OpenFOAM setup using mean drag coefficient, mean base-pressure coefficient and Strouhal number. The simulated values are consistent with experimental trends over Re = 200-400.</em></p>


# Baseline POD-DL Prediction without Adaptation

The first test evaluates the original POD-DL surrogate without adaptive correction. This baseline is useful because it shows why online adaptation is needed.

## Case Re = 200

At Re = 200, the wake exhibits an organized periodic vortex-shedding pattern. The leading POD modes capture the dominant coherent structures, and the predicted probe signals reproduce the main oscillatory behavior of velocity and pressure. The predicted amplitude and phase remain reasonable over a finite prediction window.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_Comparison_Re200.png?raw=true" alt="Comparison for Re=200 baseline POD-DL prediction" width="60%">
</p>

<p style="text-align: center;"><em>Figure 4. Comparison between prediction and CFD ground truth at probe location (0.5D, 0.5D, 0) for the flow past a circular cylinder at Re=200.</em></p>

However, the RMSE gradually increases as the prediction horizon extends. The error growth is especially visible for the streamwise and cross-stream velocity components. This confirms that even for a relatively regular wake regime, small autoregressive errors accumulate over time.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_RMSE_Re200.png?raw=true" alt="RMSE for Re=200 baseline POD-DL prediction" width="60%">
</p>

<p style="text-align: center;"><em>Figure 5. RMSE evolution for the baseline POD-DL prediction at Re = 200. The model captures the main periodic dynamics, but the error gradually increases during long-horizon autoregressive forecasting.</em></p>

## Case Re = 300

At Re = 300, the wake becomes more complex. The prediction still captures the dominant oscillatory behavior, but the mismatch grows faster than in the Re = 200 case.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_Comparison_Re300.png?raw=true" alt="Comparison for Re=200 baseline POD-DL prediction" width="30%">
</p>

<p style="text-align: center;"><em>Figure 6. Comparison between prediction and CFD ground truth at probe location (0.5D, 0.5D, 0) for the flow past a circular cylinder at Re=300.</em></p>

The RMSE also increases as the prediction horizon extends, and the error increases in comparison to Case Re=200.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_RMSE_Re300.png?raw=true" alt="RMSE for Re=300 baseline POD-DL prediction" width="60%">
</p>

<p style="text-align: center;"><em>Figure 7. RMSE evolution for the baseline POD-DL prediction at Re = 300. Compared with Re = 200, the prediction mismatch grows more rapidly because the wake dynamics are less regular and more modal content is required.</em></p>

These results show that a purely offline POD-DL surrogate is not sufficiently robust for extended forecasts when the wake dynamics become more complex.


# Scheduled Adaptive Prediction

The scheduled adaptive strategy recalls CFD after a fixed number of predicted snapshots. In the representative test, the model is trained using an initial interval, predicts the next interval, then CFD is recalled to generate new snapshots and retrain the surrogate.

The updated model significantly reduces the RMSE in the second prediction stage compared with the non-adaptive baseline. In particular, the errors of the main velocity components are effectively reset after retraining and then evolve again from a lower baseline.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_RMSE_Re300_adaptive.png?raw=true" alt="RMSE for scheduled adaptive prediction at Re=300" width="60%">
</p>

<p style="text-align: center;"><em>Figure 8. RMSE evolution for scheduled adaptive prediction at Re = 300. The transparent curves indicate the non-adaptive baseline, while the highlighted curves show the adaptive prediction. After CFD recall and retraining, the prediction error is reduced in the second forecast stage.</em></p>


The method also preserves key wake statistics, including:

- mean and fluctuation level of turbulent kinetic energy,
- temporal correlation of the streamwise velocity,
- overall evolution of the wake dynamics.

For a representative **200-snapshot** interval, the CFD computation requires 15906.9 s using 60 CPU cores, while the surrogate workflow requires 2591.7 s using 4 CPU cores. After normalizing by CPU core count, the effective speed-up is approximately **92 times** relative to CFD.


# Event-triggered Divergence Detection

Although scheduled updating is simple, it may recall CFD too early or too late because the update time is fixed in advance. The event-triggered strategy is more flexible because it links CFD recall directly to the reliability of the ongoing prediction.

In this mode, three POD-DL predictors are trained with different random seeds. Their prediction spread provides an ensemble uncertainty indicator. A dynamic threshold is estimated from the recent uncertainty history. When the uncertainty exceeds this threshold persistently, the prediction is considered unreliable.

The results show that the uncertainty trigger is consistent with physically meaningful degradation. The raw uncertainty signal is noisy, so a smoothed signal is used to identify robust trends. When the smoothed ensemble uncertainty rises above the dynamic threshold, the forecast is terminated and CFD is recalled. This avoids the need for future CFD ground-truth data during online prediction.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_Event_Triggered_Prediction.png?raw=true" alt="Event-triggered uncertainty monitoring" width="90%">
</p>

<p style="text-align: center;"><em>Figure 9. Event-triggered divergence detection based on ensemble uncertainty. The dashed green curves show raw uncertainty, the solid green curves show smoothed uncertainty, and the dashed yellow curves show the dynamic threshold. CFD is recalled when the uncertainty exceeds the threshold persistently.</em></p>

This strategy provides a practical online solution when future CFD reference data are unavailable. It allows the surrogate to continue when the prediction is stable, and automatically switches back to CFD when the reduced-order forecast becomes unreliable.


# Adaptive Prediction under Varying Inlet Velocity

A more demanding test is performed under time-varying inlet velocity. The inlet velocity changes during prediction according to: 1 → 2 → 0.8 → 1.5 m/s.

This corresponds to a Reynolds-number range of approximately **160-400**. The case represents a realistic scenario where the operating condition changes during simulation.

The ensemble uncertainty increases sharply after each inlet-velocity change. This rise in uncertainty triggers termination of the current surrogate forecast and recall of the CFD solver. The boundary condition is then updated, new CFD snapshots are generated, and the surrogate is retrained.

After retraining, the predicted drag and lift histories recover physically expected trends. This demonstrates that the adaptive framework can track regime changes and maintain predictive reliability under evolving operating conditions.

<p style="text-align: center;">
    <img src="https://github.com/modelflows/modelflowsapp/blob/research/CFD/Accelerate_CFD/assets/img/Adaptive_Inlet_Variation.png?raw=true" alt="Adaptive prediction under varying inlet velocity" width="90%">
</p>

<p style="text-align: center;"><em>Figure 10. Adaptive prediction under varying inlet velocity. The inlet velocity changes from 1 to 2, then to 0.8 and 1.5 m/s. The uncertainty indicator rises after each regime change, triggering CFD recall and surrogate retraining.</em></p>


# Key Findings

The main findings can be summarized as follows:

- **Baseline POD-DL prediction is accurate over a finite horizon**, but autoregressive errors grow gradually during long-time forecasting.
- **Scheduled adaptive updating reduces accumulated error** by periodically recalling CFD and retraining the surrogate.
- **Event-triggered updating provides an online reliability mechanism** based on ensemble uncertainty, without requiring future CFD ground truth.
- **The adaptive framework can handle changing inlet conditions**, because uncertainty rises after regime changes and activates targeted CFD recall.
- **The closed-loop CFD-surrogate workflow provides strong acceleration**, with an effective speed-up of approximately 92 times for a representative 200-snapshot interval.


# CFD-Surrogate Pipeline

This research can be organized as a reproducible workflow for adaptive prediction:

1. **Generate CFD snapshots**
   - Run OpenFOAM for an initial short interval.
   - Save velocity and pressure fields at selected sampling times.

2. **Construct the POD representation**
   - Mean-center the snapshot matrix.
   - Apply singular value decomposition.
   - Retain the dominant POD modes and temporal coefficients.

3. **Train the POD-DL predictor**
   - Standardize modal coefficients.
   - Train an LSTM-based temporal predictor.
   - Use rolling-window autoregressive forecasting.

4. **Monitor prediction reliability**
   - Run ensemble predictors with different random seeds.
   - Compute energy-weighted uncertainty in POD space.
   - Estimate a dynamic threshold using recent uncertainty history.

5. **Recall CFD when needed**
   - Stop the surrogate forecast when divergence is detected.
   - Restart OpenFOAM from the accepted predicted state or updated operating condition.
   - Generate new high-fidelity snapshots and retrain the surrogate.

# Tutorials

The tutorial for this adaptive prediction workflow is available below:

- [Tutorial: Adaptive CFD–POD–LSTM Pipeline](../../../_tutorials/2026-accelerateCFD-tutorial.md)

# Related Publication

Zou, X., Zhao, Z., Barragán, G., & Le Clainche, S. (2026). *Divergence-aware adaptive prediction framework for accelerating CFD simulations of unsteady flows*. arXiv. [https://doi.org/10.48550/arXiv.2605.24150](https://doi.org/10.48550/arXiv.2605.24150)

Abadía-Heredia, R., Zou, X., Lopez-Martin, M., & Le Clainche, S. (2025). *An adaptive framework for autoregressive forecasting in CFD using hybrid modal decomposition and deep learning*. arXiv. [https://doi.org/10.48550/arXiv.2505.01531](https://doi.org/10.48550/arXiv.2505.01531)


