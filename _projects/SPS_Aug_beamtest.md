---
title: ITS3 WP3 Testbeam @ SPS 26 - 31 July 2023
use_math: true
---

## To-do list
- [ ] ICESTICK 재프로그램 (Miko가 펌웨어 버전 확인해주기로 함)
- [ ] DUT 연결하고 테스트
- [ ] TRG/BUSY 채인 연결하고 드라이 실행 수행
- [ ] 컨트롤룸에 PC(pcepaid02) 준비(eudaq과 root 설치))

## 요약
- 참석자:
- 타겟: APTS
- 문서: [elog](https://alpide.cern.ch/its3/2023-July-SPS/)
- 데이터:
  - EOS: /eos/project/a/aliceits3/ITS3-WP3/Testbeams/2023-07-SPS
  - [CERNBox](https://cernbox.cern.ch/files/spaces/eos/project/a/aliceits3/ITS3-WP3/Testbeams/2023-07-SPS?tiles-size=1&items-per-page=100&view-mode=resource-table)

## 실험 셋업

### 빔

### Telescope B1 - APTS

![실험 테이블]({{ site.baseurl }}{% link theme/img/testbeam/Setup_table.png %}){: width="100%"}

- B1 셋업 다이어그램

![실험 다이더그램]({{ site.baseurl }}{% link theme/img/testbeam/Setup_diagram.png %}){: width="100%"}

## 로그
21st Jul. 2023
11:00
- `pcepaiddtlab2`에 테스트빔 폴더가 만들어짐
- 모든 관련된 소프트웨어와 펌웨어들이 복사됨
- 모든 필수적인 룰들이 추가되거 적용됨(`make -j prc` 동안 에러가 발생, MOSS 칩 관련 에러)
- 테스트 텔레스코프에 사용될 모든 케이블들 확인

12:00
- PMT 홀더와 PMT A0860004가 텔레스코프에 설치됨
  - TRG 보드, CH2에 연결
  - PMT가 반응하는 것을 확인 - 더 많은 테스트는 드라이 런에서)
  - 모든 파워 서플라이 채널이 설치되고 테스트되고 라벨링됨
- 파워 서플라이 채널 지도
  - PS 6 (023844922):
    - Ch1: APTS DUT DAQ
      - 전압: 5V
      - 전류상한: 900mA
      - 전압상한: 5.5V
      - 퓨즈 연결: Ch4
    - Ch2: 사용안함
    - Ch3: 사용안함
    - Ch4: APTS DUT VBB
      - 전압: 변동 가능(현재 0V)
      - 전류상한: 1mA
      - 전압상한: 5V
      - 퓨즈 연결: Ch1
  - PS 20 (019726820):
    - Ch1: HUB
      - 전압: 18V
      - 전류상한: 800mA
      - 전압상한: 19V
    - Ch2: PMT
      - 전압: 12V
      - 전류상한: 100mA
      - 전압상한: 13V
      - 퓨즈 연결: Ch3
    - Ch3: PMT
      - 전압: 12V
      - 전류상한: 100mA
      - 전압상한: 13V
      - 퓨즈 연결: Ch2
  - PS 31 (VCP120249)
    - Ch1: REF DAQ
      - 전압: 5V
      - 전류상한: 3A
      - 전압상한: 5.5V
      - 퓨즈 연결: Ch2
    - Ch2: REF VBB 
      - 전압: 3V (마이너스 안 적혀 있는 거 확인)
      - 전류상한: 1mA
      - 전압상한: 3.3V
      - 퓨즈 연결: Ch1
    - Ch3: APTS TRG DAQ
      - 전압: 5V
      - 전류상한: 900mA
      - 전압상한: 5.5V
      - 퓨즈 연결: Ch4
    - Ch4: APTS TRG VBB
      - 전압: -1.2V
      - 전류상한: 1mA
      - 전압상한: 5V
      - 퓨즈 연결: Ch3
  
13:00
- PTH 연결됨
- ZABER 스테이지 연결 및 테스트완료
- 모든 케이블 라벨링 완료
- 외부 HUB가 hub로 연결했을 때 터미널에서 찾을 수 없는 에러 발생
- PTH 테스트 결과
  - 압력: 963.61 hPa
  - 온도: 25.36 $\mathrm{^oC}$
  - 상대습도: 52.07%
  
14:00
- ALPIDE에 대한 문턱값 튜닝
- 실험 셋업 표에 정리

15:00, 17:00
- TRG 홀더, TRG 센서가 텔레스코프에 설치됨
- TRG 테스트 결과 목적하는 데로 작동됨 (게인 분석 결과를 보려면 /home/palpidefs/TB_SPS_JULY_2023/TRG_scan_TB_prep 참조)
- 트리거 용도의 DAQ 보드와 Proximity 보드는 바뀔 것이고 관련 작업은 다시 수행해야함

