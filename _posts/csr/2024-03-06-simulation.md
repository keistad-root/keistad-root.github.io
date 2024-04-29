---
title: Simulation Results
tags:
  - Cluster size
use_math: true
---

Setting and simulation results are shown. The specific explanation is located the end of this page.

## Setting

## Results

### Doubled cluster
For calculating the frequency of occuring double cluster, let two particles comes into $1mm^2$ area.
From the previous experiments, the largest cluster size of a particle is 40 pixels.
The area of pixel is $784\mathrm{\mu m^2}$ because of the pixel pitch is $28 \mathrm{\mu m}$.
Thus the maximum area of a cluster is $31360 \mathrm{\mu m^2} = 3.136 \times 10^{-2} \mathrm{mm^2}$.
Therefore the maximum radius of a cluster is obtained as $\sqrt {3.136 \times 10^{-2} \mathrm{mm^2} / pi} = 9.9991 \times 10^{-2} \mathrm{mm}$.
It is same proposition that two clusters considered as a cluster(doubled cluster) with a distance between two centre of cluster is smaller then twice of cluster radius.
The probability of the distance is smaller than diameter is extra of the distance is larger than diameter.
Ignoring the border problem for convenience, later can be easily calculated by the ratio between total area and extra area excluding the circle area with the radius is diameter of cluster.
Thus the probability is $(1\mathrm{mm^2} - \pi \times (9.9991 \times 10^{-2} \mathrm{mm^2} / 1\mathrm{mm^2})) = (1\mathrm{mm^2}-0.125\mathrm{mm^2})/1\mathrm{mm^2} = 0.87456$.
Finally, the probability of doubled cluster by two simultaneously incdented particles is $1-0.87456=0.12544$.
Generally the probability of doubled cluster by n particles incdent to $1\mathrm{mm^2}$ area simultaneously is $1-(0.87456)^n$.

By GEANT4 simulation, n can be determined by Monte-Carlo method.
It is necessary to know that the number ofparticles passed silicon detector and ther positions.
From the min and max x and y value, the radius of incidenting particles area is defined as $(|maxX-minX|+|maxY-minY|) / 4$, so the incident area is $\pi [(|maxX-minX|+|maxY-minY|) / 4]^2$.
Thus the density of particle is $(the number of particle) / [\pi [(|maxX-minX|+|maxY-minY|) / 4]^2]$.
In real experiment, if particles incident to detector during $250\mu s$, the particles considered as simultaneous particle.
Thes the number of particle incidented simultaneously is revealed as $250 \mu s \times [(\sharp\,particle) / [\pi [(X_{Mm}+Y_{Mm}) / 4]^2]]/[(\sharp\,source\,particle)/(Activity)]$.
The n value and the probability of doubled cluster is shown as following table.

|Distance <br> (source - detector)|$\phi$ of collimater|Air pressure|# particle|Area   |n          |Probability|
|:-------------------------------:|:------------------:|:----------:|:--------:|:-----:|:---------:|:---------:|
|2mm                              |1mm                 |1bar        |652       |7.13556|0.000391476|5.24698e-05|
|2mm                              |2mm                 |1bar        |5693      |26.6347|0.000915752|0.000122735|
|2mm                              |3mm                 |1bar        |17404     |65.9188|0.00113116 |0.000151603|
|2mm                              |4mm                 |1bar        |36707     |112.129|0.00140255 |0.000187972|
|3mm                              |1mm                 |1bar        |609       |19.569|0.000133332 |1.78709e-05|
|3mm                              |2mm                 |1bar        |5541      |84.7368|0.000280157|3.755e-05  |
|3mm                              |3mm                 |1bar        |17038     |173.147|0.000421588|5.65058e-05|
|3mm                              |4mm                 |1bar        |36514     |1265.67|0.000123602|1.65668e-05|
|4mm                              |1mm                 |1bar        |615       |35.4487|7.43294e-05|9.96264e-06|
|4mm                              |2mm                 |1bar        |5478      |149.687|0.000156792|2.10153e-05|
|4mm                              |3mm                 |1bar        |17153     |691.408|0.00010629 |1.42464e-05|
|4mm                              |4mm                 |1bar        |35404     |1548.16|9.79763e-05|1.31321e-05|



## Geant4 Simulation
The purpose of this simulation is to calculate the deposite enrgy of alpha, beta and gamma in ALPIDE silicon detector.
ALPIDE can be devided by two parts, circut part and collection part.
The deposit energy in each parts would be a clue to explain the cluster size distribution in ALPIDE.
Firstly the program construction will be shown and after the simulation results are displayed.

## Program Construction
The Geant4 simulation for cluster size research consists of 8 parts, i.e. 8 header and source file and 1 main executable.
Each files take care of "DetectorConstruction", "PrimaryGenerator", "ActionInitialization", "RunAction", "EventAction", "TrackingAction", "SteppingAction" and "AnalysisManager".
The "DetectorConstruction" set the geometry of simulation by making logic volumes and place the physical volume based on logic volumes.
Particle informations are put with "PrimaryGenerator" firstly, but the real properties is controlled by command line added in "DetectorConstruction".
Each actions controlling the simulation during run time is initialized in "ActionInitialization".
The actions are concerned to "Run", "Event", "Tracking" and "Stepping".
Run is a cycle of executing program.
The run is collection of event, which starts a particle like alpha, beta or gamma generating and ends all particles related to the particle generated at the start of event disappear or go out of boundary of world. 
The step is recorded when a particle feel any changes like turning its direction, generating secondary particles or losing energy.
Track action is slightly different with other actions because it participates in recording track informations.
All informations collectecd from the actions should be recorded and manufactured to readable file.
"AnalysisManager" make a file with root extension, and record informations to the file.
The details are described in the following sub-sections.

### Detector Construction
The basic function of "DetectorConstructin" is creating logical volumes and place each volumes in the form of physical volume.
For making logical volumes, solid volume for shape and material information for properties is needed.
If logic volume have complex shape, then several solid volumes combined by union or subtraction with each other.
The materials can be alhemized from basic elements, which compsed to molecule.

In this program, there are five logic volumes which are named as Stand, Shield, ALPIDEcircuit, ALPIDEEpitaxial and CarrierBoard.
The material is stand is plastic made from propenoic acid.
Because the molecular formula of propenoic acid is C3H4O2, Carbon, hydrogen and Oxygen is added.
It's density is $1.210\mathrm{g/cm^3}$, but 3D printer fill 30% instead of 100% by setting, the value is $0.3 \times 1.210\mathrm{g/cm^3}$.
The colour is set as white which rgb colour is 255, 255, 255.
In real set-up, there are several types of stand according to the experiment purpose.
The stand type can be set by macro which choose the solid volume to input the logical volume.

The shield is added for alpha screen test. 
By the stand type, the aluminium foil block the line which pass the centre of source and detector.
The depth of shiled is $1\mathrm{mm}$.
Its element is aluminium and the density is $2.7\mathrm{g/cm^3}$.
The colour is gray of 211, 211, 211.

In the introduction, it is described that ALPIDE is devided to two parts. 
The deposit energies are recorded separately but they are certainly contained in one body.
The program make two logical volumes and integrate to one assembly.
The shape of each parts is box.
Both width, depth is $3\mathrm{cm}$, $1.5\mathrm{cm}$ but the height is $11\mathrm{\mu m}$ of ALPIDEcircuit and $39\mathrm{\mu m}$ of ALPIDEEpitaxial.
The material is silicon and density is $2.33\mathrm{g/cm^3}.
The colour is yellow of 255, 255, 0.

The carrier board, PCB, has very complex material. 
It is roughly considered as mixture of fibrous glass and epoxy resin.
The fibrous glass is component of 7 kinds of molecules, 60% SiO2, 11.8% Al2O3, 0.1% Fe2O3, 22.4% CaO, 3.4% MgO, 1.0% Na2O and 1.3% TiO2.
The density of fibrous glass is $2.74351\mathrm{g/cm^3}$.
The epoxy resin which is more simple than fibrous glass is made from 38 of carbon, 40 of hydrogen, 6 of oxygen and 4 of Bromine.
The density is $1.98281\mathrm{g/cm^3}$.
The 53% of fibrous glass and 47% epoxy resin fused to one PCB, which density is $1.98281\mathrm{mg/cm^3}$
The colour is set as green of 0, 100, 0.

The commands for macro are set in this stage.
It is possible to set particle type and their energy.
The stand type and distance from source and detector are also defined here.
The air pressure can be determined by macro.


### Primary Generator Action
In here, the default particle gun is written.
The default particle type is alpha and it is $14\mathrm{mm}$ far away from detector.
The default particle gun should be set although it is regenerate by macro.

### Analysis Manager
The ActionInitialization and other actions have no special things compared to tutorials.
But the informations that would be stored is listed in AnalysisManager.
The results file contain three trees, tSource, tStepper and tTrack.
In tSource, initial value of kind, kinetic energy, position, direction and amount of primary particle are stored.
In stepping stage, the kind, kinetic energy and direction of particle, and pre/post volumes and positions and total ionizing dose and non-ionizing energy loss are recorded.
Lastly, particle ID, position and direction of particle and the number of volume and energy loss and even whether any particle pass the volume or not could be known by tTrack tree.
The energy loss histograms of tTrack tree must be crucial to analyse cluster size of ALPIDE.



