---
title: Simulation Results
tags:
  - Cluster size
use_math: true
---

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

## Results
