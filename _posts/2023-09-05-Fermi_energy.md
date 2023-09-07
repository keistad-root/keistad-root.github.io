---
title: 도핑과 페르미 에너지의 상관관계
tags:
  - 페르미 에너지
  - 고체물리학
use_math: true
---

페르미 준위($E_F$)는 절대영도에서 바닥부터 전자를 채웠을 때 가장 높은 에너지 준위를 뜻한다. 
예를 들어 3차원 공간에서 자유 전자의 페르미 기체를 가정해보자.
슈뢰딩거 방정식은 다음과 같다.

$-{\hbar^2 \over 2m}\left({\partial^2 \over \partial x^2}{\partial^2 \over \partial y^2}{\partial^2 \over \partial z^2}\right)\psi_k(r)=\epsilon_k\psi_k(r)$

이 방정식의 솔루션은

$ \psi_k(\boldsymbol{r}) = e^{i\boldsymbol{k}\cdot\boldsymbol{r}}$

이며, 고유 에너지는 다음과 같다.

$ {\hbar^2 \over 2m}\left(k_x^2+k_y^2+k_z^2\right)=\epsilon_k={\hbar^2k^2 \over 2m}$

여기서 $k$의 최대값이 페르미 운동량 $k_F$이다. 
k-공간에서 구의 부피는 ${4\over3}\pi k_F^3$이고 복셀 부피 $\left({2\pi \over L}\right)^3$으로 나눠주면 각 상자의 개수이고 각 상자당 전자가 2개가 들어가므로

$ 2 \times { {4 \over 3} \pi k_F^3 \over \left({2\pi \over L}\right)^3} = N = Vk_F^3/3\pi^2 $

$ k_F = \left({3\pi^2N\over V}\right)^{1/3} $

이므로, 페르미 에너지는

$ \epsilon_F = {\hbar^2 \over 2m}\left({3\pi^2 N \over V}\right)^{2/3} $

이다. 하지만 이는 0K에서 페르미 에너지이고 온도의 효과를 넣어주게 되면 조금 달라진다.
유한한 온도($T\ne0\mathrm{K}$)에서 전자의 에너지는 다음과 같은 페르미-디락 분포를 적용해 줘야 한다. 

$ f(\epsilon)={1 \over e^{(\epsilon - \mu)/k_BT}+1} $

이 때 $\mu$는 케미컬 퍼텐셜을 의미한다.
실재 전자의 에너지 분포는 페르미-디락 분포에 고체의 에너지띠를 곱해주면 된다.

실리콘 내에서는 페르미 에너지가 달라진다. 
실리콘에는 전자가 존재할 수 있는 허용띠가 있다.
이 때 원자 하나가 속박하고 있는 허용띠 중 가장 에너지 준위가 높은 영역대의 띠를 원자가띠(valance band)라 하고, 바로 다음 영역대의 띠를 전도띠(conduction band)라고 한다.
순수한 실리콘 반도체의 경우 페르미 준위가 원자가띠와 전도띠의 정중앙에 위치한다.
그러나 실리콘 반도체에 불순물이 섞이기 시작하면 페르미 준위가 이동을 한다.
n도핑이 많이 될 수록 페르미 준위가 전도띠에 가까워지고, p도핑이 많이 될 수록 페르미 준위가 원자가띠에 가까워진다.

![페르미 준위 변화]({{site.baseurl}}{% link theme/img/semiconductor.png %}){: width="100%"}

만약 서로 다른 타입의 두 반도체를 접합한다면, 페르미 준위를 동일하게 놓고 전도띠와 원자가띠를 그려넣으면 된다.
다음 그림을 참고하자.

![p-n 결합]({{site.baseurl}}{% link theme/img/pn_junction.png %}){: width="80%"}

이 경우 N 타입 반도체의 전도띠에 있는 전자가 P 타입 반도체로 옮겨 가려고 해도 퍼텐셜 에너지 장벽에 막히기 때문에 이동하지 못 한다.
그림과 같은 경우 퍼텐셜과 전기장 등을 구할 수 있지만 여기서는 생략하도록 하자.
즉 이러한 특성들을 잘 살펴보면 반도체 소자를 물리적으로 설명 가능하다.