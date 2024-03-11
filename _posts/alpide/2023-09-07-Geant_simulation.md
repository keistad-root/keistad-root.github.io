---
title: 실험실실험 Geant4 시뮬레이션
tags:
  - Geant4
  - Simulation
  - ALPIDE
---

개선사항
- 그림에 축 제목 그리기
- 제목 Lossed->Lost

Geant4 시뮬레이션에서는 총 5개 구역으로 나누어서 에너지를 얼마나 잃었는 지 확인했다.
각 구역은 공기(Air), 시준기(Collimeter), 회로부(circuit), 검출부(Epitaxial+Substrate), 케리어보드(Carrier board)로 나누었다. 


- 공기 중
  - 9mm

![9mm Air]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 9mm_air.pdf %})

  - 14mm

![14mm Air]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 14mm_air.pdf %})

  - 19mm

![19mm Air]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 19mm_air.pdf %})

  - 24mm

![24mm Air]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 24mm_air.pdf %})

  - 29mm

![29mm Air]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 29mm_air.pdf %})

  - 34mm

![34mm Air]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 34mm_air.pdf %})

- 진공 중 (7.5mbar)
  - 9mm

![9mm Vacuum]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 9mm_vacuum.pdf %})

  - 14mm

![14mm Vacuum]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 14mm_vacuum.pdf %})

  - 19mm

![19mm Vacuum]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 19mm_vacuum.pdf %})

  - 24mm

![24mm Vacuum]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 24mm_vacuum.pdf %})

  - 29mm

![29mm Vacuum]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 29mm_vacuum.pdf %})

  - 34mm

![34mm Vacuum]({{site.baseurl}}{% link theme/img/pid/Simulation/Simulation Result at 34mm_vacuum.pdf %})

공기 중과 진공중에서 크게 주목할만한 부분은 확실히 공기 중에서 잃는 에너지의 차이가 크다는 것이다.
공기 중 데이터를 보면 에너지를 잃는 군을 두 종류로 나눌 수 있는데, 처음 2 피크는 공기 중에서 모두 공통적으로 잃는 에너지이다. 
마지막 피크는 거리가 멀어질 수록 더 많은 에너지를 잃는 것을 확인할 수 있다.
콜리메이터의 경우 진공 중에서는 공기 중에서 에너지를 잃지 않은 입자들이 콜리메이터에 그대로 도착한 후 콜리메이터 안에서 멈춘다.
따라서 대부분의 입자들이 기여된 에너지 그대로 전부 잃은 것을 확인할 수 있다.
공기 중에서는 에너지를 어느정도 잃은 입자들이 콜리메이터에 도착하고 검출기 간 거리가 달라져도 콜리메이터까지 거리는 달라지지 않으므로 개형에 차이가 없다.

케리어보드에 도착한 입자들이 잃은 에너지부터 먼저 보면, 9mm일 때는 대부분의 입자들이 ALPIDE에 들어가므로 케리어보드에는 도착하지 않아 검출이 되지 않는 것이 정상이다.
하지만 공기 중에서 거리가 멀어질 수록 에너지가 작은 알파입자들이 케리어보드에 도달하므로 잃은 전체 에너지가 작아진다.
진공중에서는 에너지를 잃지 않고 케리어보드에 도착하기 때문에 상술한 이유로 9mm를 제외한 나머지에서는 부여된 모든 에너지를 잃는다.

이제 회로 부분에서 잃은 에너지를 보자.
공기 중에서 9mm에서는 알파가 그나마 적게 에너지를 잃기 때문에 상대적으로 란다우 분포에 가까운 분포를 보인다.
하지만 거리가 멀어질수록 에너지를 크게 잃는 입자들이 많아지고, 급기야 24mm에 가서는 분포 자체가 달라진다.
그러나 진공에서는 에너지를 잃지 않으므로 란다우 분포를 그대로 유지하고 전체 엔트리만 감소하는 것을 확인할 수 있다.

마지막으로 실제 클러스터를 형성하는 데 기여하는 검출부에서 잃는 에너지는 진공중에서는 마찬가지로 개형은 같고 엔트리만 감소한다.
하지만 공기중에서는 거리가 커질수록 이미 에너지를 많이 잃었으므로 점점 적은 에너지를 잃다가 급기야 29mm 이후부터는 검출되지 않는다.

중이온물리실험실에서 개발한 QUPID는 Geant4 시뮬레이션 중 검출부에서 잃은 에너지를 이용해서 검출기에서 전자가 얼마나 발생하는 지 예상한다.
그리고 그 예상값을 이용해서 가우스 분포로 픽셀 내에서 얼마나 퍼지는 지 계산한 다음, 문턱값을 넘는 픽셀 개수를 세는 방식으로 클러스터 사이즈를 예측한다.
그에 대한 자세한 이야기는 다른 포스트에서 논의하겠다.