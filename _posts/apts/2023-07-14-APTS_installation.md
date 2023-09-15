---
title: APTS 설치 및 운용
tags:
  - MLR1
  - APTS
  - ALICE
use_math: true
---
<!--

## APTS 초기 시험
APTS를 처음 받게 되면 초기 성능을 확인하기 위한 절차가 있다.
먼저 저항을 측정하고 전원을 공급해서 APTS까지 전류가 잘 공급되는 지 확인한다.
그리고 각 픽셀의 펄스 신호를 확인해서 각 픽셀이 정상작동하는 지 점검한다. 
해당 영역에서는 APTS의 저항 측정과 펄스 측정 등의 초기 시험 절차를 기술한다.

### 저항 측정
초기 저항 측정은 간단히 4개 채널만 시험한다. 
멀티미터를 이용하여 다음 4가지 지점 간의 저항을 측정한다.

![측정 위치]({{ site.baseurl }}{% link theme/img/apts/APTS_resistance.png %}){: width="40%"}

다음은 부산대에서 진행된 저항 측정의 결과이다.

| 단위($\mathrm{k \Omega}$) | AVSS | AVDD | PWell | PSub |
|:---:|:---:|:---:|:---:|:---:|
| AVSS | - | 63.30 | 46.52 | 43.14 |
| AVDD | 2.64 | - | 41.04 | 37.57 |
| PWell	| >2$\mathrm{M\Omega}$ | >2$\mathrm{M\Omega}$ | - | 8.59 |
| Sub | >2$\mathrm{M\Omega}$ | >2$\mathrm{M\Omega}$ | 6.72 | - |

해당 측정값이 PWell-Psub간 저항이 $\mathrm{k\Omega}$ 단위이고 나머지 저항 크기가 2$\mathrm{k\Omega}$이상이면 정상이다.

### 초기 작동 및 펄스 측정
- 하드웨어 설정
  - 파워 서플라이 설정
    - 파워 채널 
      - 전압: $5\mathrm{V}$
      - 전류 상한: $900\mathrm{mA}$ 
      - 퓨즈 딜레이: $100\mathrm{ms}$
      - 전압 상한: $6\mathrm{V}$
    - Vbb 채널
      - 전압: $0\mathrm{V}$
      - 전류 상한: $1\mathrm{mA}$ 
      - 퓨즈 딜레이: $100\mathrm{ms}$
      - 전압 상한: $5\mathrm{V}$
      - 역전압을 걸어줘야 한다는 것을 명심하자.
    - 두 채널의 퓨즈를 연결한다.
  - DAQ 보드를 주변 기기(파워 서플라이 및 컴퓨터)와 연결한다.
    - DAQ 보드에 모든 점퍼가 올바르게 연결되어 있는 지 확인한다.([mlr1 daq firmware](https://gitlab.cern.ch/alice-its3-wp3/apts-dpts-ce65-daq-fpga-firmware))
    - PWR 커넥터를 파워 채널과 연결한다.
    - Pwell과 Psub는 2to1 LEMO 커넥터를 이용하여 Vbb 채널에 연결한다. 이 때 [필터보드](https://twiki.cern.ch/twiki/bin/view/ALICE/ITS3WP3FilterVbb)를 중간에 연결해줘야 하며 극성에 유의하여 연결한다.
    - USB 케이블을 통해 컴퓨터와 연결한다.
  - 프록시미티 보드를 DAQ 보드에 연결한다.
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
![펄스 0.0Vbb]({{ site.baseurl }}{% link theme/img/apts/pulse_00.png %}){: width="80%"}

- 4.8Vbb를 걸어줬을 때 펄스의 절대값과 그 개형
![펄스 4.8Vbb]({{ site.baseurl }}{% link theme/img/apts/pulse_48.png %}){: width="80%"}
-->