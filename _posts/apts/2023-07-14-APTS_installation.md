---
title: APTS Basic operation
tags:
  - MLR1
  - APTS
  - ALICE
use_math: true
---

## APTS initial test
The procedure of initial test of APTS is checking inital performance such likes resistance of chips and electric test.
In this section, the methods for measuring resistance and current is shown.
And the pulses are given to APTS and checking output signals.

### Resistance measurement
There are brief test and detail test in resistance measurement.
In the brief test, the only 4 channels in APTS are tested.
It can be measured by multimeter.

The next table is results of resistance measurement.

| Unit($\mathrm{k \Omega}$) | AVSS | AVDD | PWell | PSub |
|:---:|:---:|:---:|:---:|:---:|
| AVSS | - | 63.30 | 46.52 | 43.14 |
| AVDD | 2.64 | - | 41.04 | 37.57 |
| PWell	| >2$\mathrm{M\Omega}$ | >2$\mathrm{M\Omega}$ | - | 8.59 |
| Sub | >2$\mathrm{M\Omega}$ | >2$\mathrm{M\Omega}$ | 6.72 | - |

The level of resistance between Pwell and Psub should be $\mathrm{k \Omega}$ and other resistance should be larger than $2\mathrm{k \Omega}$.

### Inital operation and pusle measurement
- Setting hardwares
  - Power supply
    - Power channel
      - Voltage: $5\mathrm{V}$
      - Current upper-limit: $900\mathrm{mA}$ 
      - Fuse delay: $100\mathrm{ms}$
      - Voltage upper-limit: $6\mathrm{V}$
    - Vbb channel
      - Voltage: $0\mathrm{V}$
      - Current upper-limit: $1\mathrm{mA}$ 
      - Fuse delay: $100\mathrm{ms}$
      - Voltage upper-limit: $5\mathrm{V}$
      - Keep in mind that the back-bias voltage should be taken to chip.
    - Connect the fuse of power and Vbb channel
  - Connect DAQ board to sub-devices. (Power supply and computer)
    - Checking the all jumpers correctively pluged on DAQ board.([mlr1 daq firmware](https://gitlab.cern.ch/alice-its3-wp3/apts-dpts-ce65-daq-fpga-firmware))
    - Connect PWR connector to power channel.
    - Pwell and Psub are connected to Vbb channel using 2to1 LEMO connector. [Filter board](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3FilterVbb) is plugged between LEMO connector and Vbb channel for removing noise. One more checking polarity.
    - Connect to computer via USB cable.
  - Plug proximity board to DAQ board.
    - Check the jumper is pluged to correct position. (Refer to [mlr1 daq firmware](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3FilterVbb) J3->Isa(It doesn't exist on proximity board v2.), J5->TEMP)
  - Connect chip carrier board to [proximity board](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3MLR1TestSystem)
  - Isolate expeirment setup from light source.
- Pulse measurement on 0 VBB
  - Turn on Vbb channel and power channel.
    - Reference current on power channel $\sim 370\mathrm{mA}$
    - Reference current on VBB channel $<0.1\mathrm{mA}$
  - Install fx3 and fpga via `mlr1-daq-program --fx3 path-to/fx3.img --fpga path-to/0xXXXXXX.bit`.
    - Check the version of fpga.bit is laatest. (Check [Firmware](https://twiki.cern.ch/twiki/bin/view/ALICE/MLR1DAQBoardFirmware))
    - Reference current on power channel $\sim 415\mathrm{mA}$
    - Reference current on VBB channel $<0.1\mathrm{mA}$
  - Suppy power to APTS chip via `python apts_power_on.py PROXIMITY_VERSION`.
    - $5 \mathrm{mA} <$ $I_a$(Print on terminal) $< 7 \mathrm{mA}$
      - In case of multiplexer APTS, about $21\mathrm{mA}$ is printed out as analogue current.
    - Reference current on VBB channel $<0.1\mathrm{mA}$
  - Execute `python test_pulsing.py PROXIMITY_VERSION CHIP_ID -p f` to give pulse.
    - Check the pulse signal is printed out for all pixels.
    - Reference current on power channel $\sim 720\mathrm{mA}$
    - Reference current on VBB channel $<0.1\mathrm{mA}$
    - Check the shape of pusle and amplitude value.
  - Power of the chip via `apts_power_off.py`.
  - Turn of power channel and VBB channel.
- - Pulse measurement on high VBB
  - Turn on Vbb channel and power channel.
    - Reference current on power channel $\sim 370\mathrm{mA}$
    - Reference current on VBB channel $<0.1\mathrm{mA}$
  - Install fx3 and fpga via `mlr1-daq-program --fx3 path-to/fx3.img --fpga path-to/0xXXXXXX.bit`.
    - Check the version of fpga.bit is laatest. (Check [Firmware](https://twiki.cern.ch/twiki/bin/view/ALICE/MLR1DAQBoardFirmware))
    - Reference current on power channel $\sim 415\mathrm{mA}$
    - Reference current on VBB channel $<0.1\mathrm{mA}$
  - If VBB is indicated 0V, then increase VBB to 4.8V with step as 0.3V.
    - Reference current on VBB channel $<0.5\mathrm{mA}$
  - Suppy power to APTS chip via `python apts_power_on.py PROXIMITY_VERSION`.
    - $5 \mathrm{mA} <$ $I_a$(Print on terminal) $< 7 \mathrm{mA}$
      - In case of multiplexer APTS, about $21\mathrm{mA}$ is printed out as analogue current.
    - Reference current on VBB channel $<0.5\mathrm{mA}$
  - Execute `python test_pulsing.py PROXIMITY_VERSION CHIP_ID -p f` to give pulse.
    - Check the pulse signal is printed out for all pixels.
    - Reference current on power channel $\sim 720\mathrm{mA}$
    - Reference current on VBB channel $<0.5\mathrm{mA}$
    - Check the shape of pusle and amplitude value.
  - Power of the chip via `apts_power_off.py`.
  - Turn of power channel and VBB channel.

### Result
- The amplitude and shape of pulse when 0.0VBB

- The amplitude and shape of pulse when 4.8VBB