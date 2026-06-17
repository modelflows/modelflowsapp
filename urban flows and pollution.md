---
layout: page
title: Urban Flows and Air Pollution
subtitle: Our studies focused on urban flows
published: false
---

Codes available:

1. [Calibration of Low-Cost Air Quality Sensors](https://modelflows.github.io/modelflowsapp/urbanflows_airpollution/#calibration-of-low-cost-air-quality-sensors)

---

## Calibration of Low-Cost Air Quality Sensors <a id="calibration-of-low-cost-air-quality-sensors"></a>

Low-cost air quality sensors (LCS) provide a practical alternative to regulatory-grade instruments, enabling dense monitoring networks in urban environments. Their deployment, however, is constrained by calibration challenges related to sensor drift, environmental cross-sensitivity, and device-to-device variability. This section presents a deep learning based calibration framework built around a Long Short-Term Memory (LSTM) model trained on co-located reference measurements. The model operates on a structured input space that combines lagged sensor and meteorological variables with harmonic encodings of diurnal and seasonal cycles, as well as interaction terms. By combining both temporal memory and cyclic structure into the learning process, the approach captures short-term dynamics and long-term trends in pollutant behaviour.

![Calibration Methodology](https://github.com/modelflows/modelflowsapp/blob/master/assets/img/2025_15_12_Sengupta_Calibration_Methodology.png)
*Code in progress…*

