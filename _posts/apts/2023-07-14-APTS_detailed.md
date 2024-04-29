---
title:  APTS basic description
tags:
  - MLR1
  - APTS
  - ALICE
use_math: true
---


## Background
APTS is short form of Analogue Pixel Test Structure.
It is designed in ITS3 upgrade project.
The main goal of ITS3 upgrade project is decreasing a material budget of inner tracking system.
TowerJazz 180nm technology is adopted to a previous tracker, ITS2.
In ITS3, new technology with 65nm is choosen, so 65nm thechnology should be tested.
Thus the MLR1 chipset was designed for testing the characteristic of 65nm technology.
There are many chips in MLR1 such like DPTS, CE65, etc.
In this chpter, however, the description focuses on APTS chip.

## Naming rule
There are many variants in APTS.
They can be classified by circuitary, pixel pitch and MAPS structure. 
The details of each feature are described in following sub-sections.

### Circuitary
Totally three circuit types, F, A and O are designed to APTS.
F is basic source follower circuit.
It provides strong analogue readout but very slow.
And the output signal is smaller than input signal because it doesn't have any amplifier.
The tested chip has type F circuitary.

The inner amplifier is added to basic source follower structure between pixel fornt-end and source-follower chain in type A.
The gain of type A APTS has higher gain than type F by amplifier.
It can be devided two sub-types, DC coupled and AC coupled.

In type O, high-speed OpAmp is used as amlifier and it attached output parts out of pxiel.
It has high quality timing performance and provides $50\mathrm{\Omega}$ terminal resistance to board.
The fornt-end is same with source follower structure.

### The pixel pitch
The definition of pixel pitch is the distance between collection diodes of two adjacent pixels.
It can be considered as the size of pixel.
APTS has four different pixel pitch, $10 \mathrm{\mu m}$, $15 \mathrm{\mu m}$, $20 \mathrm{\mu m}$ and $25 \mathrm{\mu m}$.
The active shape of APTS is 4 times 4 matrix.
The pixel pitch of Pusan APTS is $15 \mathrm{\mu m}$.
Thus its active area is $60 \mathrm{\mu m} \times 60 \mathrm{\mu m}$

### MAPS structure
MAPS is short form of Monolithic Active Pixel Sensor.
In the ALPIDE chip used in previous ITS system, the MAPS strucure is adopted for increasing readout speed.
If a particle incidents to ALPIDE, then it deposits its energy to silicon of ALPIDE.
The energy ionizes the silicon structure and makes electron hole pairs.
The free electrons move freely in epitaxial layer out of depleted region.
And if they reach to boundary of depleted region, then they feel electric field that the direction is outward of n-type collection diode.
It means that the electrons inside of boundary of depleted region are collected to collection diode.

Although the MAPS structre is very nice, it can be evolved.
The type B, or modified, is filled with deep low dose n-type implant.
The full pixel area is covered with n-type implant.
It makes strong electric field in epitaxial layer, so the depleted region of modified type is larger than standard type.
This will increase Charge Collection Efficiency and imporve radiation hardness.

The type P is that the chip is modified with gap.
It means the low dose n-type implant doesn't cover edge of pixel that the size is $1.25\mathrm{\mu m}$.
This makes lateral electric field on the edges of pixels.
The radiation hardness is improved in this region.
The Pusan chip has type P MAPS structure.
