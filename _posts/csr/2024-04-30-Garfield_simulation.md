---
title: Garfield simulation
---

Garfield simulation is made for testing silicon detector or gas chamber like TPC against to high energy particles from colliding point.
A biggest difference between high and low energy incident particle is energy loss.
The high energy particles lose few energy, it means that decreasing momentum of particle is ignorable.
The alpha particle from 241Am, however, deposit all of their energy to silicon detector and stop there.

The methods for generating track of primary particle in Garfield are HEED, SRIM&TRIM and Degrade.
HEED is basic tracker of Garfield, but it is for high energy particles.
So the magnitude of momentum of particle doesn't change in simulation, although the energy loss of particle is calculated.
Srim&Trim is external tool for calculating energy loss and including change of particle speed.
It heard that Srim&Trim is proper for this analysis, but it is half right and half wrong.
This tool is only supported on Window XP.
Converting operation system is not recommended.
The last one, Degrade, is for x-ray and beta particle.
It cannot analyse alpha particle.

Fortunately, Garfield simulation can be combined with Geant4 simulation.
It is needed to make new physics in Geant4 with electric field and doping information.
The big problem is simulation rate.
The burden is extremly high for this job.
Using KIAF for parallel computing is considerable.