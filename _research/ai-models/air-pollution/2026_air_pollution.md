---
layout: post
category: "Data-driven & Urban Sustainability"
topic: "Air Pollution"
thumbnail: "[https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-1.jpg]"
tldr: "Urban Energy Efficiency Assessment under Uncertainty."
title: Sustainable Cities & Energy Systems 
subtitle: Our studies focused on urban sustainability
---
<p class="post-meta">
  Posted on 18 June 2026
</p>

## Introduction
Rapid urbanization and economic growth have significantly increased energy demand across Chinese cities, creating new challenges related to sustainability, resource management, and environmental performance. Under the framework of China's carbon neutrality objectives, understanding how efficiently cities utilize energy resources has become increasingly important for supporting sustainable development policies.
This study evaluates the energy efficiency of 280 Chinese prefecture-level cities under uncertainty conditions, providing a robust framework to assess urban energy performance while accounting for data variability and measurement uncertainty.

## Study Area
The analysis considers 280 prefecture-level cities distributed across China's seven major regions: North China, Northeast China, Central China, East China, South China, Southwest China, and Northwest China.
This large-scale dataset enables the investigation of regional disparities in energy efficiency and the identification of long-term development patterns across different economic and geographical contexts.
<p align="center">
  <a href="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-6.png?raw=true">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-6.png?raw=true"
         alt="vel_plot"
         width="650">
  </a>
</p>

## Research Methodology

Research Methodology
Robust Data Envelopment Analysis (RDEA)
Data Envelopment Analysis (DEA) is a widely used non-parametric approach for evaluating the relative efficiency of Decision-Making Units (DMUs). However, conventional DEA models assume deterministic input and output variables, making their results sensitive to measurement errors and data uncertainty.
To overcome this limitation, this work integrates Robust Optimization (RO) into the DEA framework through the Robust Data Envelopment Analysis (RDEA) methodology.
By introducing uncertainty sets and protection levels, RDEA evaluates efficiency under worst-case scenarios, producing more reliable and stable efficiency estimates.
Two robust formulations are considered:

- CU-RDEA (Conservative Uncertainty Robust DEA)
- CEU-RDEA (Conservative Extended Uncertainty Robust DEA)

This approach allows the assessment of how uncertainty affects urban energy efficiency rankings and regional performance.
<p align="center">
  <a href="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-7.png?raw=true">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-7.png?raw=true"
         alt="vel_plot"
         width="700">
  </a>
</p>

The diagram should show how urban energy data are processed through DEA and Robust Optimization to build the CU-RDEA and CEU-RDEA models. The goal is to communicate the novelty of the methodology rather than reproduce the mathematical formulation presented in the article.

## Main Findings

The results reveal that urban energy efficiency is highly sensitive to data uncertainty.
As the perturbation level (Γ) increases, both CU-RDEA and CEU-RDEA efficiency scores show a systematic decline, demonstrating the importance of incorporating uncertainty into efficiency assessments.
The analysis also highlights substantial regional disparities across China:

- East China exhibits the highest overall efficiency levels.
- Northwest and Southwest China show comparatively lower efficiency performance.
- Significant spatial heterogeneity exists among cities within the same region.
- 
Furthermore, the results indicate a progressive transition from traditional resource-driven development models toward growth supported by technological innovation, industrial upgrading, and green low-carbon strategies.
<p align="center">
  <a href="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-8.png?raw=true">
    <img src="https://github.com/modelflows/modelflowsapp/blob/dev/assets/img/2026-workshop-li-urban-8.png?raw=true"
         alt="vel_plot"
         width="8500">
  </a>
</p>

The figure should clearly illustrate (i) regional differences in urban energy efficiency and (ii) the impact of uncertainty levels (Γ) on efficiency scores. A China efficiency map combined with a regional comparison chart would communicate the results more effectively for a web audience than the full set of detailed regional plots

## Scientific Contribution
This work demonstrates that Robust Data Envelopment Analysis provides a reliable framework for evaluating urban energy efficiency under uncertainty.
By combining DEA and Robust Optimization, the proposed methodology reduces sensitivity to data fluctuations and offers a more realistic assessment of urban sustainability performance.
The framework can support policy evaluation, urban planning, energy management, and sustainable development strategies in complex socio-economic systems.

## Scientific Contribution

This work demonstrates that Robust Data Envelopment Analysis provides a reliable framework for evaluating urban energy efficiency under uncertainty.
By combining DEA and Robust Optimization, the proposed methodology reduces sensitivity to data fluctuations and offers a more realistic assessment of urban sustainability performance.
The framework can support policy evaluation, urban planning, energy management, and sustainable development strategies in complex socio-economic systems.

## Relevance for ModelFLOWs

This research illustrates the application of advanced data-driven methodologies to large-scale urban systems.
Beyond traditional engineering applications, ModelFLOWs methodologies can be used to analyze complex socio-economic and environmental datasets, enabling robust decision-support tools for sustainability, smart cities, and energy planning.

## References

Jian Li, Soledad Le Clainche, and collaborators.
A Robust Cross-Efficiency DEA Model with Undesirable Outputs for Urban Energy Efficiency Evaluation.
Manuscript in preparation.



