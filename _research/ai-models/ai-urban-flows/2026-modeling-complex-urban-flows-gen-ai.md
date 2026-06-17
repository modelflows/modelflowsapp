---
layout: post
title: "Modeling complex urban flows with generative AI"
category: "AI & Data-Driven Models"
topic: "AI for Urban Flows"
thumbnail: "/assets/img/urban-flows/diffusion_scheme.png"
tldr: "Geometry-aware flow generation and sensor-informed data assimilation for urban wind fields."
---

---

# Generative Modeling and Data Assimilation for Urban Wind Flows

Urban wind flows are central to air-quality assessment, pedestrian comfort, heat dispersion, and climate-resilient urban design. However, resolving wind fields in realistic city geometries remains computationally demanding. High-fidelity CFD simulations can require large unstructured meshes, many wind directions, and substantial HPC resources, which limits their use in rapid scenario exploration, digital twins, and operational decision support.

In this project, we develop **geometry-aware generative models for urban airflow** that operate directly on unstructured CFD meshes.

We organize the work into two complementary methods:

1. **Flow prior generation from geometry only**  
   Generation of plausible steady urban wind fields using only the urban mesh and inflow direction.

2. **Generative data assimilation using sparse observations**  
   Reconstruction of high-resolution wind fields by combining a learned flow prior with sparse sensor measurements.

Together, these methods provide a path toward fast, uncertainty-aware urban flow prediction and reconstruction in complex urban domains.

---

## Method 1: Flow Prior Generation from Geometry Only

The first method addresses the following question:

> Can we generate physically plausible urban wind fields using only the city geometry and the incoming wind direction?

In our first work, **Generative Urban Flow Modeling: From Geometry to Airflow with Graph Diffusion** (Giral et al.), we propose a graph-based diffusion model for synthesizing steady-state urban wind fields on unstructured meshes.

The model requires only geometry-related inputs:

- mesh connectivity,
- node coordinates,
- node labels such as wall, boundary, and fluid nodes,
- and the global inflow wind direction.

At inference time, the method does not require sensor observations, previous flow snapshots, or reduced-order coefficients.

### Architecture

<!-- Replace this path with the actual figure path in your GitHub repository -->
<p align="center">
  <img src="{{ 'assets/img/urban-flows/graph_structure_scheme.png' | relative_url }}" alt="Graph diffusion architecture" width="800"/>
</p>

<p align="center">
  <em>
  Hierarchical message passing architecture used by the graph denoiser. Local updates are performed on the original high-resolution mesh, while a reduced mesh enables efficient long-range information propagation. Features are then projected back to the original CFD mesh, where the final velocity field is generated.
  </em>
</p>

The denoiser follows a multiscale graph neural network design. It combines message passing on both the original mesh and a reduced mesh. This allows the model to preserve local obstacle-aware detail while propagating long-range flow information across the urban domain.

<!-- Replace this path with the actual figure path in your GitHub repository -->
<p align="center">
  <img src="{{ 'assets/img/urban-flows/diffusion_scheme.png' | relative_url }}" alt="Diffusion denoising process" width="800"/>
</p>

<p align="center">
  <em>
  Overview of the diffusion generation process. Starting from noise, the model progressively denoises the velocity field while conditioning on the urban mesh, node types, and inflow wind direction.
  </em>
</p>

### Dataset and Setup

The dataset is built from steady-state RANS simulations of a realistic urban neighborhood. The original 3D CFD domain contains detailed buildings, irregular terrain, and a large unstructured mesh. Horizontal slices are extracted at multiple heights, producing different 2D unstructured meshes with varying building configurations.

Each slice contains flow fields for multiple inflow wind directions. Some slices are used for training, while others are reserved for testing on unseen geometries.

<!-- Replace this path with the actual figure path in your GitHub repository -->
<p align="center">
  <img src="{{ 'assets/img/urban-flows/gensynth_train_tes.png' | relative_url }}" alt="Training and testing urban meshes" width="800"/>
</p>

<p align="center">
  <em>
  Training and test meshes differ in obstacle configuration and mesh resolution. The model receives only mesh information and inflow direction, then generates the corresponding velocity field.
  </em>
</p>

### Results

The model generates coherent urban flow structures across unseen geometries and wind directions. It recovers dominant inflow patterns, shear gradients near buildings, recirculation zones, and wake structures downstream of obstacles.

<!-- Replace this path with the actual figure path in your GitHub repository -->
<div style="display: flex; justify-content: center; gap: 10px;">
  <img src="{{ 'assets/img/urban-flows/zoom_z35_angle46_Ux.png' | relative_url }}" alt="Velocity component Ux" width="400"/>
  <img src="{{ 'assets/img/urban-flows/zoom_z35_angle46_Uy.png' | relative_url }}" alt="Velocity component Uy" width="400"/>
</div>

<p align="center">
  <em>
  Comparison between CFD ground truth and generated velocity components (Ux and Uy) showing detailed structures in a dense urban region. The generated fields reproduce velocity decay inside street canyons and strong gradients near building edges.
  </em>
</p>

The generated fields also reproduce important statistical properties of the CFD data. Probability density comparisons and modal analyses show that the generated samples preserve both bulk velocity distributions and dominant coherent flow structures.

<!-- Replace this path with the actual figure path in your GitHub repository -->
<p align="center">
  <img src="{{ 'assets/img/urban-flows/pdf_comparison_speed_angle171_z35.png' | relative_url }}" alt="Statistical validation of generated fields" width="800"/>
</p>

<p align="center">
  <em>
  Statistical validation of the generated flow fields. The diffusion-GNN model reproduces both bulk velocity distributions and dominant energetic structures across unseen test cases.
  </em>
</p>

---

## Method 2: Generative Data Assimilation Using Sensor Observations and a Learned Prior

The second method addresses a complementary question:

> Can we reconstruct a full high-resolution urban wind field from sparse sensor observations?

In our second work, **GenDA: Generative Data Assimilation on Complex Urban Areas via Classifier-Free Diffusion Guidance** (Giral et al.), we introduce a generative data assimilation framework that combines a learned geometry-aware flow prior with sparse observations.

The unconditional branch learns plausible urban wind fields from geometry, while the sensor-conditioned branch incorporates measurements during sampling.

### Architecture

<!-- Replace this path with the actual figure path in your GitHub repository -->
<p align="center">
  <img src="{{ 'assets/img/urban-flows/generative_data_assimilation.png' | relative_url }}" alt="GenDA architecture" width="800"/>
</p>

<p align="center">
  <em>
  GenDA reconstructs high-resolution wind fields from sparse observations using classifier-free diffusion guidance. The unconditional branch provides a geometry-aware prior, while the sensor-conditioned branch injects observational constraints during sampling.
  </em>
</p>

This formulation interprets classifier-free guidance as a learned posterior reconstruction mechanism. Instead of treating sparse observations as a separate correction step, the model integrates sensor information directly into the generative sampling process.

This allows the reconstruction to remain consistent with both:

- the available sensor observations,
- and the physical constraints encoded by the urban geometry and learned flow prior.

### Observation Settings

GenDA is designed to work with different observation configurations, including:

- **sparse fixed sensors**, representing stationary monitoring stations placed in the domain;
- **trajectory-based observations**, representing measurements collected along moving paths.

Both cases use the same reconstruction procedure, enabling flexible deployment scenarios for environmental monitoring.


### Results

GenDA reconstructs high-resolution urban wind fields on unseen geometries, wind directions, and mesh resolutions without retraining. Compared with supervised graph neural network baselines and classical reduced-order data assimilation methods, the method improves both pointwise accuracy and structural reconstruction quality.

<!-- Replace this path with the actual figure path in your GitHub repository -->
<p align="center">
  <img src="{{ 'assets/img/urban-flows/angle_253_4x4_obs2177.png' | relative_url }}" alt="Sparse sensor observation settings" width="800"/>
</p>

<p align="center">
  <em>
  High-resolution wind-field reconstruction from sparse observations. GenDA recovers obstacle-aware flow structures, including wakes and recirculation zones, while remaining consistent with available sensor measurements.
  </em>
</p>


This approach is especially useful when full CFD simulations are unavailable in real time, but sparse sensor measurements are available from urban monitoring networks, mobile platforms, or short observational campaigns.

---

## Why These Two Methods Are Complementary

The two methods form a natural sequence.

**Flow prior generation** learns the distribution of physically plausible urban wind fields from geometry and wind direction alone.

**Generative data assimilation** uses that learned prior and updates it with sparse observations to reconstruct the most plausible full-field state.

The first method supports rapid what-if simulation for urban planning, while the second supports real-time or near-real-time environmental monitoring when partial measurements are available.

---

## Applications

These tools can support:

- rapid wind-comfort assessment in complex urban districts;
- air-quality and pollutant-dispersion studies;
- sensor-informed urban digital twins;
- uncertainty-aware environmental monitoring;
- fast scenario exploration for urban planning and emergency response.

---

## Code and Data Availability

**Code and tutorials:** coming soon.  
**Data:** coming soon.

---

## References

Francisco Giral, Álvaro Manzano, Ignacio Gómez, Petros Koumoutsakos, and Soledad Le Clainche.  
**Generative Urban Flow Modeling: From Geometry to Airflow with Graph Diffusion.**  
arXiv:2512.14725, 2025.  
[https://arxiv.org/abs/2512.14725](https://arxiv.org/abs/2512.14725)

Francisco Giral, Álvaro Manzano, Ignacio Gómez, Ricardo Vinuesa, and Soledad Le Clainche.  
**GenDA: Generative Data Assimilation on Complex Urban Areas via Classifier-Free Diffusion Guidance.**  
arXiv:2601.11440, 2026.  
[https://arxiv.org/abs/2601.11440](https://arxiv.org/abs/2601.11440)