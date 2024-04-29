---
title: APTS 설치 및 운용
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
    - 점퍼가 올바른 위치에 꽂혀 있는 지 확인한다. ([mlr1 daq firmware](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3FilterVbb) J3->Isa(프록시미티 보드 v2에는 존재하지 않음), J5->TEMP)
  - 칩 캐리어 보드를 [프록시미티 보드](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3MLR1TestSystem)에 연결한다.
  - 광원으로 부터 실험 셋업을 고립시킨다.
- 0Vbb에서 펄스 측정
  - Vbb 채널과 파워 채널을 켠다.
    - 파워 채널 전류 $\sim 370\mathrm{mA}$
    - Vbb 채널 전류 $<0.1\mathrm{mA}$
  - fx3와 fpga를 `mlr1-daq-program --fx3 path-to/fx3.img --fpga path-to/0xXXXXXX.bit`을 이용해서 설치한다.
    - 최신 fpga .bit 버전을 가지고 있는 지 확인 ([펌웨어](https://twiki.cern.ch/twiki/bin/view/ALICE/MLR1DAQBoardFirmware) 확인)
    - 파워 채널 전류 $\sim 415\mathrm{mA}$
    - Vbb 채널 전류 $<0.1\mathrm{mA}$
  - `python apts_power_on.py PROXIMITY_VERSION`를 이용해서 칩에 전원을 공급한다.
    - $5 \mathrm{mA} <$ $I_a$ 전류 (터미널에 출력) $< 7 \mathrm{mA}$
      - 멀티플렉서 칩의 경우 $21\mathrm{mA}$ 정도의 값이 출력된다.
    - Vbb 채널 전류 $<0.1\mathrm{mA}$
  - `python test_pulsing.py PROXIMITY_VERSION CHIP_ID -p f`를 실행한다.
    - 모든 픽셀에 대해 시그널이 출력되는 지 확인한다.
    - 파워 채널 전류 $\sim 720\mathrm{mA}$
    - Vbb 채널 전류 $<0.1\mathrm{mA}$
    - 펄스의 개형과 절대값을 확인한다.
  - `apts_power_off.py`을 이용해서 칩의 전원을 끈다.
  - 파워 채널과 Vbb 채널을 끈다.
- 높은 Vbb에서 펄스 측정
  - Vbb 채널과 파워 채널을 켠다.
    - 파워 채널 전류 $\sim 370\mathrm{mA}$
    - Vbb 채널 전류 $<0.1\mathrm{mA}$
  - fx3와 fpga를 `mlr1-daq-program --fx3 path-to/fx3.img --fpga path-to/0xXXXXXX.bit`을 이용해서 설치한다.
    - 최신 fpga .bit 버전을 가지고 있는 지 확인 ([펌웨어](https://twiki.cern.ch/twiki/bin/view/ALICE/MLR1DAQBoardFirmware) 확인)
    - 파워 채널 전류 $\sim 415\mathrm{mA}$
    - Vbb 채널 전류 $<0.1\mathrm{mA}$
  - 0 Vbb에서 측정을 하였다면, Vbb를 4.8V까지 0.3V씩 증가시킨다.
    - Vbb 채널 전류 $<0.5\mathrm{mA}$
  - `python apts_power_on.py PROXIMITY_VERSION`를 이용해서 칩에 전원을 공급한다.
    - $5 \mathrm{mA} <$ $I_a$ 전류 (터미널에 출력) $< 7 \mathrm{mA}$
      - 멀티플렉서 칩의 경우 $21\mathrm{mA}$ 정도의 값이 출력된다.
    - Vbb 채널 전류 $<0.5\mathrm{mA}$
  - `python test_pulsing.py PROXIMITY_VERSION CHIP_ID -p f`를 실행한다.
    - 모든 픽셀에 대해 시그널이 출력되는 지 확인한다.
    - 파워 채널 전류 $\sim 720\mathrm{mA}$
    - Vbb 채널 전류 $<0.5\mathrm{mA}$
    - 펄스의 개형과 절대값을 확인한다.
  - `apts_power_off.py`을 이용해서 칩의 전원을 끈다.
  - 파워 채널과 Vbb 채널을 끈다.

### 실험 결과
- 0.0Vbb를 걸어줬을 때 펄스의 절대값과 그 개형

- 4.8Vbb를 걸어줬을 때 펄스의 절대값과 그 개형
