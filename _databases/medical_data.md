---
layout: post
title: "Medical data"
type: "Experimental / Cardiac"
tldr: "Cardiac data used for cardiovascular disease research"
---

### Data index:
   * [Ideal Left Ventricle](#cardiac-ideal-lv)
   * [EchoNet-Dynamic](#cardiac-echonet-dynamic)
   * [PhysioNet - Phonocardiogram Dataset 2026](#cardiac-phonocardiograms)

## Cardiac Flow Ideal Left Ventricle <a id="cardiac-ideal-lv"></a>
This database contains data from a three-dimensional CFD simulation of incompressible, Newtonian blood flow inside an idealized left ventricular cavity. The flow is laminar, with a Reynolds number of 5500. The simulation was conducted using Ansys Fluent version 2024R2.

If you use this dataset in your work, please cite:  

Lazpita, E., Mares, A., Quintero, P., Garicano-Mena, J., & Le Clainche, S. (2024). *Modeling heart flow dynamics using numerical simulations to identify the vortex ring: a practical guide.* Results in Engineering, 24, 103644.  
DOI: [https://doi.org/10.1016/j.rineng.2024.103644](https://doi.org/10.1016/j.rineng.2024.103644)  

Database available [here](https://drive.google.com/drive/folders/1WJOnLmLEolYZcJiAcayVAO9AEwgv3pfu?usp=sharing).

## EchoNet-Dynamic <a id="cardiac-echonet-dynamic"></a>
The EchoNet-Dynamic database is a public dataset published by Stanford University, which includes 10,030 labeled A4C echocardiogram videos and human expert annotations (measurements, tracings, and calculations) to provide a baseline to study cardiac motion and chamber sizes.
You can find the database and the code at https://echonet.github.io/dynamic/

## PhysioNet - Phonocardiogram Dataset 2026 <a id="cardiac-phonocardiograms"></a>
This dataset contains 4430 recordings from 1297 patients, 2435 recordings from 764 patients for training and 1277 recordings from 308 patients for testing.
All the data comes from 9 differents databases which gives PhysioNet more variabiliy. The recordings takes a time between 5 and 122 seconds, and are resampled to 2000 Hz.

The database, it is a binary classification between **normal** and **abnormal** patients.

[[Link to Physionet](https://physionet.org/content/challenge-2016/1.0.0/#files-panel)]