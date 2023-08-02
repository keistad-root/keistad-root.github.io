---
title:  APTS 기본 설명
tags:
  - MLR1
  - APTS
  - ALICE
use_math: true
---

## 배경
APTS는 ITS3 업그레이드 계획 중에 개발된 검출기이다.
ITS3의 주요 목표는 물질량을 줄이는 것과 충돌 지점에 보다 가깝게 검출기를 배치하는 것이다.
이 때 물질량을 줄이기위한 계획의 일환으로 회로를 더 세밀하게 인쇄하는 것이 있다.
이렇게 되면 검출기에서 소비되는 전력을 줄여 발열을 제거하여 냉각 시스템으로 물을 사용하지 않을 수 있다.
기존 ALPIDE에서는 TaworJazz 회사의 180nm 공정을 사용하였다. 
이 때 회로를 더 세밀하게 인쇄하기 위해 65nm공정을 채택하기로 하였다.
따라서 이러한 65nm 공정을 검증하기 위하여 MLR1 칩셋이 개발되게 되었다.
여기서 APTS는 이러한 칩셋에 배치된 검출기 중 하나이다.

## 명명법
APTS에는 다양한 변종들이 있으며 회로, 픽셀 면적, MAPS 구조 등에 따라 크게 나뉜다.
이러한 특성들의 조합에 따라 APTS에는 총 44가지의 변종들이 존재한다.
따라오는 세부 세션에서는 각 특성들의 설명을 간단히 소개한다.

### 회로
APTS의 회로 종류에는 크게 F(basic source follower), A(source follower structure with in-pixel amplifier), O(OPAMP)가 있다.

![F 타입]({{ site.baseurl }}{% link theme/img/apts/basic source follower.png %}){: width="40%"}

F 타입은 강력한 아날로그 리드아웃을 제공하나 느리다.
그리고 증폭기가 없기 때문에 출력 신호가 입력 신호보다 작다.

![A 타입 DC]({{ site.baseurl }}{% link theme/img/apts/DC coupled amplifier.png %}){: width="40%"}
![A 타입 AC]({{ site.baseurl }}{% link theme/img/apts/AC coupled amplifier.png %}){: width="40%"}

A 타입은 기본 소스 팔로워 구조 기반에 픽셀 프론트-엔드와 소스 팔로워 체인 전에 픽셀 내부 증폭기가 달려있다.
증폭기에 의해 높은 게인이 A 타입의 특징이다.
A 타입은 다시 DC 커플드 타입과 AC 커플드 타입으로 나뉜다. 

![O 타입]({{ site.baseurl }}{% link theme/img/apts/Opamp.png %}){: width="40%"}

O 타입은 고속의 OpAmp가 바깥 출력부에 달려 있는 것으로 더 좋은 타이밍 퍼포먼스와 $50\mathrm{\Omega}$ 종말 저항을 보드에 제공한다.
프론트-엔드는 소스 팔로워 구조와 동일하다.

### 픽셀 면적
APTS는 총 네 가지 픽셀 면적을 가진다.
각각의 모양은 정사각형으로 한 변의 길이가 각각 $10 \mathrm{\mu m}$, $15 \mathrm{\mu m}$, $20 \mathrm{\mu m}$ 그리고 $25 \mathrm{\mu m}$이다. 

### MAPS 구조
![MAPS 구조]({{ site.baseurl }}{% link theme/img/apts/MAPS types.png %}){: width="40%"}

기존 ITS의 MAPS구조에서는 n-well 수집 다이오드 주변으로 공핍 영역이 형성되어 입자가 지나가면서 만들어내는 전자가 자유 거동 중 공핍 영역에 도달하면 수집 다이오드로 모이는 방식을 사용하였다.
이러한 방식의 문제점은 픽셀마다 균일한 공핍 영역 제공이 불가능하고 공핍 영역과 비공핍 영역에서 입자가 발생했을 때 결과가 달라질 수도 있다.
따라서 새로 개발되는 칩에서는 약한 n형 도핑을 추가하여 공핍영역을 픽셀 전체로 확장한다. 
이 때 n형 도핑을 추가하는 방식에는 픽셀 윗면 전체를 약한 n형 도핑을 하는 B 타입과 픽셀과 픽셀 사이에 간격을 두는 P 타입이 존재한다. 
