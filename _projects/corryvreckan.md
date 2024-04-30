---
title: Tracking system for tracking telescope in ITS3 upgrade project
---

Procedure
- Createmask
  - Masking noise pixel
- Prealign
  - Align plain with gauss fitting parameter
- Align
  - Align plain with Chi2 method
- Analyse
  - Draw DUT plots
    - Chi2 track
    - Track angle
    - Cluster information
    - Hitmap
    - Residual
    - Tracking efficiency
  
## 2020 December Data
Bent ALPIDE
![Set_up]({{ site.baseurl }}{% link theme/img/corryvreckan/Dec_2021_set_up.png %}){: width="100%"}

- Chi2
![Chi2_Fitting]({{ site.baseurl }}{% link theme/img/corryvreckan/chi2_fit.png %}){: width="100%"}

- Residual
![Residual_Fitting]({{ site.baseurl }}{% link theme/img/corryvreckan/residual_fit.png %}){: width="100%"}

- Track Angle
![Angle_fitting]({{ site.baseurl }}{% link theme/img/corryvreckan/track_angle_fit.png %}){: width="100%"}

- Cluster Size per track
![Cluster_size_per_track]({{ site.baseurl }}{% link theme/img/corryvreckan/cluster_size_per_track.png %}){: width="100%"}

## 2021 July Data
- July Track Chi2
![Chi2]({{ site.baseurl }}{% link theme/img/corryvreckan/july_track_chi2.png %}){: width="100%"}

- Skewed Residual
![Skewed_residual]({{ site.baseurl }}{% link theme/img/corryvreckan/skewed_residual.png %}){: width="100%"}

## 2021 September
DPTS
![Set_up]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_set_up.png %}){: width="100%"}

- DPTS3
![DPTS3_residual]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_dpts3_residual.png %}){: width="100%"}
![DPTS3_efficiency]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_dpts3_efficiency.png %}){: width="100%"}
- DPTS4
![DPTS4_residual]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_dpts4_residual.png %}){: width="100%"}
![DPTS4_efficiency]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_dpts4_efficiency.png %}){: width="100%"}
- Hitmap
![DPTS_hitmap]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_hitmap.png %}){: width="100%"}

걍 전체적으로 찐빠나 있음 이게 고쳐짐
- dpts에서 픽셀의 행단 위치와 종단 위치를 따로 읽어내는 데 두 값이 서로 안맞았음
  - 칼리브레이션을 통해서 해결
- prealign과 align과정을 두 번 거치면서 residual 향상

다음은 개선된 결과임
![DPTS_reformed_hitmap]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_reformed_hitmap.png %}){: width="100%"}
중간 중간 약간씩 튄다고 생각되는 픽셀들이 있음 (노이즈)

->엄청 나중에 한 거긴 하지만 이런 픽셀들은 그냥 마스킹 해줌

![DPTS_reformed_hitmap]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_dpts3_reformed_residual.png %}){: width="100%"}
![DPTS_reformed_hitmap]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_dpts4_reformed_residual.png %}){: width="100%"}

Residual도 잘 찾아 주는 것을 볼 수 있음. 하지만 Russo 결과랑 조금 다름

![DPTS_reformed_efficiency]({{ site.baseurl }}{% link theme/img/corryvreckan/sep_2021_reformed_efficiency_map.png %}){: width="100%"}


