---
layout: post
title: "Low-Cost Sensor Calibration for Air Pollution"
category: "AI & Data-Driven Models"
topic: "Air Pollution"
thumbnail: "/assets/img/air-pollution/calibration_methodology.png"
tldr: "Deep-learning-based calibration of low-cost air-quality sensors using reference measurements, meteorological variables, temporal features, and autoregressive correction."
---

---

# Low-Cost Sensor Calibration for Air Pollution Monitoring

Low-cost sensors provide an affordable way to increase the spatial density of air-quality monitoring networks. They can be deployed across urban areas at a much lower cost than reference-grade stations, making them useful for local pollution mapping, exposure assessment, and sensor-informed urban studies.

However, low-cost sensors are also affected by drift, environmental conditions, cross-sensitivity, seasonal variability, and local site effects. Their raw measurements often deviate from reference instruments, especially when temperature, humidity, traffic patterns, or background pollution levels change.

In this project, we develop **data-driven calibration methods for low-cost air-quality sensors**. The aim is to correct low-cost sensor readings using co-located reference measurements, meteorological variables, and temporal information.

We organize the calibration workflow into the following steps:

1. **Data preparation and cleaning**  
   Alignment of low-cost sensor data, reference measurements, and meteorological variables.

2. **Feature engineering**  
   Construction of lagged variables, temporal features, environmental indicators, and interaction terms.

3. **Deep-learning calibration**  
   Training of temporal models such as LSTM, GRU, and TCN-based networks.

4. **Autoregressive correction**  
   Use of previous calibrated values to improve temporal consistency during unseen-data prediction.

Together, these steps provide a complete calibration framework for improving the reliability of low-cost air-pollution sensors.

---

## Methodology

The calibration workflow starts from raw low-cost sensor measurements and reference-grade monitoring data. The two data sources are cleaned, synchronized, and transformed into a supervised learning problem. A deep-learning model is then trained to learn the correction between the low-cost sensor signal and the reference measurement.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/calibration_methodology.png' | relative_url }}" alt="Low-cost sensor calibration methodology" width="850"/>
</p>

<p align="center">
  <em>
  General methodology for calibrating low-cost air-quality sensors using reference data, meteorological variables, temporal features, and deep-learning models.
  </em>
</p>

The pipeline follows four main stages:

1. **Raw data collection**  
   Low-cost sensor readings, reference measurements, and meteorological variables are collected over the same time period.

2. **Pre-processing and filtering**  
   Missing values, abnormal readings, duplicated timestamps, and inconsistent records are removed or corrected.

3. **Temporal modelling**  
   The cleaned dataset is transformed into sequences so that the model can learn the time-dependent behaviour of the sensor.

4. **Calibrated output generation**  
   The trained model predicts the corrected pollutant concentration for unseen data.

---

## Data Preparation

The calibration dataset combines low-cost sensor readings with reference measurements and meteorological information. The data are first aligned in time so that each sensor measurement corresponds to the correct reference value and environmental condition.

Typical input variables include:

- raw low-cost sensor concentration;
- reference pollutant concentration;
- temperature;
- relative humidity;
- pressure;
- wind speed;
- wind direction;
- time of day;
- day of week;
- seasonal indicators.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/data_preparation.png' | relative_url }}" alt="Data preparation for low-cost sensor calibration" width="850"/>
</p>

<p align="center">
  <em>
  Data preparation stage, where low-cost sensor readings, reference measurements, and meteorological variables are cleaned and synchronized.
  </em>
</p>

This step is important because low-cost sensor calibration is highly sensitive to data quality. Incorrect timestamps, missing intervals, or abnormal peaks can strongly affect the final model.

---

## Feature Engineering

After cleaning, additional features are created to help the model capture the behaviour of the sensor under changing environmental and temporal conditions.

These features may include:

- lagged sensor values;
- lagged meteorological variables;
- rolling averages;
- rush-hour indicators;
- weekday and weekend indicators;
- sinusoidal time encodings;
- interaction terms between pollutant and meteorological variables.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/feature_engineering.png' | relative_url }}" alt="Feature engineering for air pollution sensor calibration" width="850"/>
</p>

<p align="center">
  <em>
  Feature engineering stage used to include temporal memory, environmental effects, and recurring daily or weekly patterns.
  </em>
</p>

The purpose of this step is to give the model enough information to distinguish between true pollution changes and sensor artefacts caused by environmental or operational effects.

---

## Sequence Generation

The calibration problem is treated as a temporal modelling task. Instead of predicting each point independently, the model receives a short sequence of previous observations and uses this history to estimate the calibrated value at the next time step.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/sequence_generation.png' | relative_url }}" alt="Sequence generation for temporal calibration" width="850"/>
</p>

<p align="center">
  <em>
  Sequence generation for temporal calibration. Past observations are used to predict the corrected pollutant concentration at the next time step.
  </em>
</p>

This approach allows the model to learn sensor memory effects, gradual drift, delayed response, and short-term pollution dynamics.

---

## Method 1: LSTM-Based Calibration

The first calibration model is based on Long Short-Term Memory networks. LSTM models are well suited for time-series calibration because they can learn dependencies across previous time steps.

The model receives a sequence of input features and predicts the calibrated pollutant concentration. Depending on the calibration setup, the model can be trained either to predict the absolute reference value or to predict the correction between the raw sensor and the reference measurement.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/lstm_calibration.png' | relative_url }}" alt="LSTM calibration architecture" width="850"/>
</p>

<p align="center">
  <em>
  LSTM-based calibration model for correcting low-cost sensor measurements using temporal and environmental information.
  </em>
</p>

### Main Features

- The model uses temporal sequences instead of isolated measurements.
- Past sensor behaviour is included in the prediction.
- Meteorological variables help correct environmental sensitivity.
- The calibrated output is compared against the reference station.
- The approach can be applied to pollutants such as PM10, PM2.5, NOx, and NO₂.

---

## Method 2: GRU and TCN Calibration Models

In addition to LSTM models, alternative temporal architectures can be used for calibration. GRU models provide a lighter recurrent structure, while Temporal Convolutional Networks use causal convolutions to model time-dependent patterns.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/gru_tcn_calibration.png' | relative_url }}" alt="GRU and TCN calibration models" width="850"/>
</p>

<p align="center">
  <em>
  Alternative temporal calibration models based on GRU and TCN architectures.
  </em>
</p>

These models are useful for comparing accuracy, training cost, stability, and generalization across different monitoring sites.

### Main Features

- GRU models are computationally lighter than LSTM models.
- TCN models can capture temporal patterns through causal convolutions.
- Different model types can be compared for each pollutant and site.
- The best-performing architecture can then be selected for deployment.

---

## Autoregressive Calibration

For unseen data, the calibrated output can be used autoregressively. This means that the previous calibrated value is included as part of the input when predicting the next calibrated value.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/autoregressive_calibration.png' | relative_url }}" alt="Autoregressive low-cost sensor calibration" width="850"/>
</p>

<p align="center">
  <em>
  Autoregressive calibration strategy, where previous calibrated values are used to improve the next prediction.
  </em>
</p>

This helps improve temporal consistency, especially when the sensor signal is noisy or when the calibration model is applied to continuous unseen periods.

The autoregressive step is particularly useful when the objective is to generate a corrected time series rather than isolated calibrated points.

---

## Ground Truth and Calibrated Measurements

The calibration quality is assessed by comparing the raw low-cost sensor signal, the calibrated model output, and the reference-grade measurement.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/ground_truth_calibration.png' | relative_url }}" alt="Ground truth and calibrated air pollution measurements" width="850"/>
</p>

<p align="center">
  <em>
  Comparison between raw low-cost sensor measurements, reference observations, and calibrated model predictions.
  </em>
</p>

The calibrated signal should follow the reference measurement more closely than the raw sensor signal. This includes both the background concentration level and short-term pollution peaks.

---

## Calibration Results

The performance of the calibration model is evaluated using standard regression metrics. These metrics compare the calibrated output against the reference measurement.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/calibration_results.png' | relative_url }}" alt="Calibration results for low-cost air pollution sensors" width="900"/>
</p>

<p align="center">
  <em>
  Calibration results showing the improvement from raw low-cost sensor measurements to corrected model predictions.
  </em>
</p>

The main goal is not only to reduce the numerical error but also to preserve the temporal behaviour of the pollutant signal. A good calibration model should correct the sensor bias while keeping the important pollution peaks and daily patterns.

---

## Error and Performance Comparison

The calibration methods are compared using error metrics, temporal stability, and generalization across test periods or monitoring sites.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/error_comparison.png' | relative_url }}" alt="Error comparison for low-cost sensor calibration" width="850"/>
</p>

<p align="center">
  <em>
  Error comparison between raw sensor measurements and calibrated model outputs.
  </em>
</p>

The calibrated model is expected to reduce the difference between the low-cost sensor and the reference instrument. The improvement can be assessed through metrics such as RMSE, MAE, correlation, bias reduction, and error distribution.

---

## Pollutants and Monitoring Sites

The calibration framework can be applied to different pollutants and monitoring sites. The same general pipeline can be reused while adjusting the input variables, time window, and model architecture for each case.

<p align="center">
  <img src="{{ 'assets/img/air-pollution/site_pollutant_overview.png' | relative_url }}" alt="Pollutants and monitoring sites for calibration" width="850"/>
</p>

<p align="center">
  <em>
  Overview of pollutants and monitoring sites used for developing and testing the calibration framework.
  </em>
</p>

This structure makes the method flexible for both single-site calibration and future multi-site generalization.

---

## Applications

These methods can support:

- calibration of low-cost air-quality sensors;
- correction of PM10, PM2.5, NOx, and NO₂ measurements;
- dense urban air-quality monitoring;
- sensor-informed pollution mapping;
- long-term sensor deployment studies;
- air-quality data quality improvement;
- urban exposure assessment;
- integration of low-cost sensors into digital-twin workflows.

---

## Code and Data Availability

**Code and tutorials:** coming soon.  
**Data:** coming soon.  
**Example notebooks:** coming soon.

---

## Related Papers

Arindam Sengupta, Soledad Le Clainche, and collaborators.  
**Deep-Learning Calibration of Low-Cost Air-Quality Sensors Using Temporal and Meteorological Features.**  
Manuscript in preparation.

---

## References

Spinelle, L., Gerboles, M., Aleixandre, M.  
**Performance Evaluation of Amperometric Sensors for the Monitoring of Ozone and Nitrogen Dioxide in Ambient Air at ppb Level.**  
Procedia Engineering, 120, 480–483, 2015.

Zimmerman, N., Presto, A. A., Kumar, S. P. N., Gu, J., Hauryliuk, A., Robinson, E. S., Robinson, A. L., Subramanian, R.  
**A Machine Learning Calibration Model Using Random Forests to Improve Sensor Performance for Lower-Cost Air Quality Monitoring.**  
Atmospheric Measurement Techniques, 11, 291–313, 2018.

Malings, C., Tanzer, R., Hauryliuk, A., Saha, P. K., Robinson, A. L., Presto, A. A., Subramanian, R.  
**Development of a General Calibration Model and Long-Term Performance Evaluation of Low-Cost Sensors for Air Pollutant Gas Monitoring.**  
Atmospheric Measurement Techniques, 12, 903–920, 2019.

Bigi, A., Mueller, M., Grange, S. K., Ghermandi, G., Hueglin, C.  
**Performance of NO, NO₂ Low Cost Sensors and Three Calibration Approaches within a Real World Application.**  
Atmospheric Measurement Techniques, 11, 3717–3735, 2018.

Karagulian, F., Barbiere, M., Kotsev, A., Spinelle, L., Gerboles, M., Lagler, F., Redon, N., Crunaire, S., Borowiak, A.  
**Review of the Performance of Low-Cost Sensors for Air Quality Monitoring.**  
Atmosphere, 10(9), 506, 2019.
