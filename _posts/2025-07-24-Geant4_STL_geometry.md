---
title: GEANT4에서 지오메트리 생성 시 CAD 파일에서 바로 불러오기
tags:
  - C++
  - Multithread
use_math: true
---

# 목적

GEANT4에서 지오메트리를 디자인하면 시간도 오래 걸리고 노력이 많이 필요하다.
그래서 Autodesk Fusion 등의 CAD 툴을 이용하여 그래픽 기반으로 설계를 하는 것이 간편하다.
따라서 CAD로 디자인한 모형을 GEANT4에 바로 넣을 수 있으면 시간을 절약할 수 있다.

# 사전 준비물 

[CADMesh](https://github.com/christopherpoole/CADMesh): STL 파일에서 GEANT4로 변환해주는 라이브러리

# 

