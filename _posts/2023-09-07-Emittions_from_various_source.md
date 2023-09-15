---
title: 다양한 선원들이 방출하는 방사선
tags:
  - Am-241
  - Sr-90
use_math: true
---
<!--

다음 글 중 241Am 내용은 [해당 논문](https://www.tandfonline.com/doi/full/10.1080/00223131.2016.1174167)을 정리한 것이다.

![241Am schematic]({{site.baseurl}}{% link theme/img/pid/241Am Schematic.png %}){:width="60%"}

아메리슘-241은 알파 붕괴를 하는 핵종으로 반감기가 432년이다.
위의 그림은 아메리슘-241이 어떻게 붕괴하는 지 간략하게 나타낸 것이다.
해당 논문에서 사용한 241Am은 AREVA사에서 제작되었다.
30mm 직경에 두께가 0.5mm인 쇠원판에 15mm 직경으로 선원이 발려있다.
활성도는 $ 352\mathrm{Bq}\pm0.5\mathrm{\%} $이다.
측정은 실리콘 검출기(BU-016-300-100)으로 관측하였으며 활성 면적이 $ 300\mathrm{mm^2} $이다. 
검출기와 선원 사이 간격은 43mm이다.

![241Am alpha-ray spectrum]({{site.baseurl}}{% link theme/img/pid/241Am alpha-ray spectrum.png %}){:width="60%"}

이 그림은 241Am 방사선원의 알파선 스펙트럼을 보여준다. 에너지 분해능은 5486keV에서 20keV 정도이다. 
5400keV에서 5600keV까지 241Am 알파선에서 유래한 네가지 픽을 관측할 수 있다. 
게다가 239Pu와 242,244Cm 불순물도 스펙트럼에서 관측된다.
이러한 불순물들의 기여도는 피크로부터 0.34%로 계산된다.
다른 불순물들은 관측되지 않는다.
측정된 검출 효율은 $ 1.141\pm0.006 $이다.

![241Am gamma-ray spectrum]({{site.baseurl}}{% link theme/img/pid/241Am gamma-ray spectrum.png %}){:width="60%"}

감마 입자의 경우 ORTEC에서 제조한 $ 36\mathrm{mm} \times 13\mathrm{mm} $ 평평한 모양의 저에너지 광자 HPGe 검출기(GLP-36360/13P4)를 사용하였다.
p 타입 저마늄 결정과 0.254mm 두께의 베릴륨창으로 구성된다. 이 때 모자-크리스탈 거리는 7mm이다. 
ORTEC에서 만든 X-COOLER III로 HPGe 검출기를 식힌다.
CANBERRA에서 만든 Lynx 디지털 신호 분석기로 HPGe에서 나온 신호를 먹인 뒤에 컴퓨터에 신호가 기록된다.
112keV에서 에너지 분해능은 0.6keV이다. 
모든 측정은 20.0cm 거리를 두고 진행되었다. 
Figure 5에서는 25시간 동안 나온 감마선 스펙트럼을 관측한 것이다. 
60keV 근처의 피크는 241Am 59.54keV 붕괴 감마선에 의한 것이다.
불확도는 26.34keV의 경우 3.6%, 59.54keV의 경우 0.75%이다.
나머지 관측되는 불순물들은 소스에서 오는 게 아닌 방배경복사이다. 

90Sr은 [여기](https://www.ld-didactic.de/software/524221en/Content/Appendix/Sr90.htm)에서 가져왔다.

![90Sr beta-ray spectrum]({{site.baseurl}}{% link theme/img/pid/90Sr beta-ray spectrum.png %}){:width="60%"}

90Sr은 28.5년의 반감기를 가진 인공 동위원소이다.
90Sr은 대다수가 90Yt으로 최대 546keV의 베타선을 방출하며 붕괴한다.
90Yt은 다시 최대 2274keV의 베타선을 방출하면서 90Zi으로 붕괴한다.
이 때 90Yt의 반감기는 64.1시간이다.