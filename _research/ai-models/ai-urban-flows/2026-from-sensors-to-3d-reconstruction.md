---
layout: post
title: From Sensors to 3D Reconstruction
category: AI & Data-Driven Models
topic: AI for Urban Flows
thumbnail: /assets/img/urban-flows/reconstruction/lcsvd_lchosvd_overview.png
tldr: Low-cost reconstruction of full 3D urban flow and pollutant fields from sparse sensor information using lcSVD and lcHOSVD.
---

# From Sensors to 3D Reconstruction

Urban flow and pollutant fields are strongly three-dimensional, especially in dense city geometries where buildings, streets, and local recirculation zones create complex spatial patterns. High-fidelity CFD simulations can resolve these effects, but storing and processing the full flow field is expensive.

This work focuses on low-cost reconstruction methods, where only a reduced set of sensor locations is used to recover the full 3D flow and pollutant field.

## Reconstruction idea

The main idea is to move from sparse sensor information to a complete spatial representation of the urban domain. Instead of decomposing the full CFD field directly, the data are first sampled at selected sensor locations. These reduced measurements are then used to construct a low-cost modal representation of the original field.

## Low-cost SVD

In the lcSVD approach, the 3D field is reshaped into a two-dimensional matrix. A reduced matrix is formed using only the selected sensor points, and singular value decomposition is applied to extract the dominant modes.

Each retained SVD mode represents a global spatial structure of the field. The reconstructed solution is obtained by combining a small number of these modes. Since only one SVD is required, lcSVD is computationally efficient and suitable for fast reconstruction.

## Low-cost HOSVD

In the lcHOSVD approach, the tensor structure of the field is preserved. The decomposition is performed separately along the spatial directions, allowing the method to retain information in the x, y, and z directions.

The reconstructed field is represented using directional modes and a compact core tensor. This makes lcHOSVD more suitable for complex three-dimensional fields, where the flow contains strong spatial interactions and localized structures.

## Comparison

lcSVD is usually faster because it applies a single decomposition to a reduced matrix. lcHOSVD is usually more accurate for complex 3D structures because it preserves the tensor form of the data and captures directional dependencies.

In simple terms, lcSVD gives a faster reconstruction, while lcHOSVD provides a more structured representation of the flow.

## Representative figures

<p align="center">
  <img src="/assets/img/urban-flows/reconstruction/lcsvd_lchosvd_overview.png" alt="Low-cost reconstruction workflow" width="85%">
</p>

<p align="center">
  <em>Workflow from sparse sensors to full 3D reconstruction using lcSVD and lcHOSVD.</em>
</p>

<p align="center">
  <img src="/assets/img/urban-flows/reconstruction/reconstruction_comparison.png" alt="Reconstruction comparison" width="90%">
</p>

<p align="center">
  <em>Comparison between the original CFD field and the reconstructed fields.</em>
</p>

## Summary

The reconstruction framework provides a low-cost path from sparse sensor data to full 3D urban flow and pollutant fields. lcSVD offers a fast matrix-based reconstruction, while lcHOSVD provides a tensor-based reconstruction that better preserves the spatial structure of the problem.
