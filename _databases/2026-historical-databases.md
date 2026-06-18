---
layout: post
title: "Fluid Dynamics Benchmark Datasets"
type: "Simulation / Legacy"
tldr: "Archive of fluid dynamics datasets including flow past cylinder, channel, jet flow, and others."
order: 1
---

If you use our databases for your studies, please reference our website with:

ModelFLOWs (2023). *ModelFLOWs-app*. Retrieved [date], from [https://modelflows.github.io/modelflowsapp/](https://modelflows.github.io/modelflowsapp/)


Databases available:
1. [Flow Past a Cylinder](#cylinder)
    * [2D Laminar Flow](#cylinder-2d)
    * [2D Laminar Flow (with 2 small cylinders)](#cylinder-2d_2)
    * [3D Laminar Flow](#cylinder-3d)
         - [Long](#cylinder-3d-long)
         - [Short](#cylinder-3d-short)

2. [Channel Flow](#channel)
    * [Plain](#channel-plain)
    * [Ribbed](#channel-rib)
    * [Cavity](#channel-cavity)

3. [Jet Flow](#jet)
   * [Concentric Jets](#jet-concentric)

4. [Cardiac Flow](#cardiac)
   * [Ideal Left Ventricle](#cardiac-ideal-lv)
  
5. [Other Geometries](#other)
   * [Planar FDA Nozzle](#FDA)


## Flow Past a Cylinder <a id="cylinder"></a>

### 2D Laminar Flow <a id="cylinder-2d"></a>
This database contains data from a two-dimensional CFD simulation of the flow past a circular cylinder. The flow is laminar, with six diferent Reynolds number of 50, 60, 85, 100, 130 and 160. The simulation was conducted using Nek5000.

![cyl2D]({{ '/assets/img/Databases/cyl2D.png' | relative_url }})

If you use this dataset in your work, please cite:  

Corrochano, A., & Le Clainche, S. (2022). Structural sensitivity in non-linear flows using direct solutions. Computers & Mathematics with Applications, 128, 69-78. DOI: [https://doi.org/10.1016/j.camwa.2022.10.006](https://doi.org/10.1016/j.camwa.2022.10.006)

Database available [here](https://drive.google.com/drive/folders/1hP1ghrAtfQb7a-ZTtw64Ambgi5WVVCRN?usp=sharing).

### 2D Laminar Flow (with 2 small cylinders) <a id="cylinder-2d_2"></a>
This database contains data from a two-dimensional CFD simulation of the flow past a circular cylinder with two small cylinders introduced in the wake of the main cylinder. The flow is laminar, with two diferent Reynolds number of 70 and 100. The simulation was conducted using Nek5000.

![CJ]({{ '/assets/img/Databases/Cyl2D_2cyl.png' | relative_url }})

If you use this dataset in your work, please cite:  

Lazpita, E., Garicano-Mena, J., Paniagua, G., Le Clainche, S., & Valero, E. (2024). A data–driven sensibility tool for flow control based on resolvent analysis. Results in Engineering, 22, 102070. DOI: [https://doi.org/10.1016/j.rineng.2024.102070](https://doi.org/10.1016/j.rineng.2024.102070)

Database available [here](https://drive.google.com/drive/folders/1ZSsYMPKdrGAs-SOgCuiblSMBvCel5xcR?usp=sharing).

### 3D Laminar Flow <a id="cylinder-3d"></a>

#### Long <a id="cylinder-3d-long"></a>
This database contains data from a two-dimensional CFD simulation of the flow past a circular cylinder. The flow is laminar, with a Reynolds number of 280 and a spanwise longitude of Lz = 6.99. The simulation was conducted using Nek5000.

![cyl3Dlong]({{ '/assets/img/Databases/cyl3Dlong.png' | relative_url }})

If you use this dataset in your work, please cite:  

Vega, J.M., & Le Clainche, S. (2020). Higher order dynamic mode decomposition and its applications. Academic Press. DOI: [https://doi.org/10.1016/C2019-0-00038-6](https://doi.org/10.1016/C2019-0-00038-6)

Database available [here](https://drive.google.com/drive/folders/1_MkWVuWWoE3hGKPT0FbCba234KJ06kQo?usp=sharing).

#### Short <a id="cylinder-3d-short"></a>
This database contains data from a two-dimensional CFD simulation of the flow past a circular cylinder. The flow is laminar, with a Reynolds number of 280 and a spanwise longitude of Lz = 1.67. The simulation was conducted using Nek5000.

![cyl3Dshort]({{ '/assets/img/Databases/cyl3Dshort.png' | relative_url }})

If you use this dataset in your work, please cite:  

Vega, J.M., & Le Clainche, S. (2020). Higher order dynamic mode decomposition and its applications. Academic Press. DOI: [https://doi.org/10.1016/C2019-0-00038-6](https://doi.org/10.1016/C2019-0-00038-6)

Database available [here](https://drive.google.com/drive/folders/1ykbsXhyrWVDBCycmD4d-UNVl9M-Os1yC?usp=sharing).

## Channel Flow <a id="channel"></a>

### Plain <a id="channel-plain"></a>
This database contains data from a two-dimensional CFD simulation of a turbulent channel flow.

![channel]({{ '/assets/img/Databases/channel.png' | relative_url }})

If you use this dataset in your work, please cite:

Lazpita, E., Garicano-Mena, J., Paniagua, G., Le Clainche, S., & Valero, E. (2024). A data–driven sensibility tool for flow control based on resolvent analysis. Results in Engineering, 22, 102070. DOI: [https://doi.org/10.1016/j.rineng.2024.102070](https://doi.org/10.1016/j.rineng.2024.102070)

Database available [here](https://drive.google.com/drive/folders/1lnNz172hU-DHKDzdVeijlRH8mEEgbGbl?usp=sharing).

### Ribbed <a id="channel-rib"></a>
This database contains data from a two-dimensional CFD simulation of a turbulent channel flow with a rib.

![rib]({{ '/assets/img/Databases/channel_rib.png' | relative_url }})

If you use this dataset in your work, please cite:

Lazpita, E., Garicano-Mena, J., Paniagua, G., Le Clainche, S., & Valero, E. (2024). A data–driven sensibility tool for flow control based on resolvent analysis. Results in Engineering, 22, 102070. DOI: [https://doi.org/10.1016/j.rineng.2024.102070](https://doi.org/10.1016/j.rineng.2024.102070)

Database available [here](https://drive.google.com/drive/folders/1dR28lDsfkW3TYXq0KM_VE9ysOC6i-YwL?usp=sharing).

### Cavity <a id="channel-cavity"></a>
This database contains data from a two-dimensional CFD simulation of a turbulent channel flow with a cavity.

![cavity]({{ '/assets/img/Databases/channel_cav.png' | relative_url }})

If you use this dataset in your work, please cite:

Lazpita, E., Garicano-Mena, J., Paniagua, G., Le Clainche, S., & Valero, E. (2024). A data–driven sensibility tool for flow control based on resolvent analysis. Results in Engineering, 22, 102070. DOI: [https://doi.org/10.1016/j.rineng.2024.102070](https://doi.org/10.1016/j.rineng.2024.102070)

Database available [here](https://drive.google.com/drive/folders/1-XvmUDFBQ5Iib6Vh-zq7-DZTnBSoh3Cz?usp=sharing).

## Jet Flow <a id="jet"></a>

### Concentric Jets <a id="jet-concentric"></a>
This database contains data from a two-dimensional CFD simulation of the flow inside two axi-symmetric concentric jets with similar velocity ratio. The flow is laminar, with a Reynolds number of 1420. The simulation was conducted using Nek5000.

![CJ]({{ '/assets/img/Databases/Concentricjets.png' | relative_url }})

If you use this dataset in your work, please cite:

Corrochano, A., & Le Clainche, S. (2022). Structural sensitivity in non-linear flows using direct solutions. Computers & Mathematics with Applications, 128, 69-78. DOI: [https://doi.org/10.1016/j.camwa.2022.10.006](https://doi.org/10.1016/j.camwa.2022.10.006)

Database available [here](https://drive.google.com/drive/folders/1EzzCI9f58FwXU2v0e8cn1ucTV3Dc56pi?usp=sharing).

## Cardiac Flow <a id="cardiac"></a>

### Ideal Left Ventricle <a id="cardiac-ideal-lv"></a>
This database contains data from a three-dimensional CFD simulation of incompressible, Newtonian blood flow inside an idealized left ventricular cavity. The flow is laminar, with a Reynolds number of 5500. The simulation was conducted using Ansys Fluent version 2024R2.

![CJ]({{ '/assets/img/Databases/LV.png' | relative_url }})

If you use this dataset in your work, please cite:  

Lazpita, E., Mares, A., Quintero, P., Garicano-Mena, J., & Le Clainche, S. (2024). *Modeling heart flow dynamics using numerical simulations to identify the vortex ring: a practical guide.* Results in Engineering, 24, 103644.  
DOI: [https://doi.org/10.1016/j.rineng.2024.103644](https://doi.org/10.1016/j.rineng.2024.103644)  

Database available [here](https://drive.google.com/drive/folders/1WJOnLmLEolYZcJiAcayVAO9AEwgv3pfu?usp=sharing).

## Other Geometries <a id="other"></a>

### Planar FDA Nozzle <a id="FDA"></a>
This database contains data from a two-dimensional CFD simulation of the flow through a planar Food and Drug Administration (FDA) nozzle, starting from the exit of the nozzle. The flow is laminar, with a Reynolds number of 800. The simulation was conducted using Nek5000.

![FDA]({{ '/assets/img/Databases/FDAnozzle.png' | relative_url }})

If you use this dataset in your work, please cite:

Corrochano, A., & Le Clainche, S. (2022). Structural sensitivity in non-linear flows using direct solutions. Computers & Mathematics with Applications, 128, 69-78. DOI: [https://doi.org/10.1016/j.camwa.2022.10.006](https://doi.org/10.1016/j.camwa.2022.10.006)

Corrochano, A., Xavier, D., Schlatter, P., Vinuesa, R., & Le Clainche, S. (2021) Flow Structures on a Planar Food and Drug Administration (FDA) Nozzle at Low and Intermediate Reynolds Number. Fluids, 6(1):4. DOI: [https://doi.org/10.3390/fluids6010004](https://doi.org/10.3390/fluids6010004)

Database available [here](https://drive.google.com/drive/folders/11nFkVnfALx-WEJCKqHJyjfXAlFTHHwQB?usp=sharing).
