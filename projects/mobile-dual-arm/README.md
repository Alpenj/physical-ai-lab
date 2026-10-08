# TJJ | 이동형 양팔 로봇 — 모방학습·시뮬레이션·Sim-to-Real

**전형주 주 담당: 양팔 태스크의 모방학습, 시뮬레이션과 Sim-to-Real.**

SO-101 양팔과 TurtleBot3 Waffle Pi를 연결해 작업 위치로 이동하고 물체를 조작하는 팀 프로젝트입니다. 저는 시연 데이터와 정책 실험, 물리 모델, 접촉·경로 검사와 실물 전이 검증을 중심으로 작업합니다. **VSLAM 모듈의 설계·구현·코드 작업에도 협업 참여했습니다.** 이동 모듈의 주 담당은 팀원 `shouttt1320`입니다.

[포트폴리오·이력서](https://julianjeonresume.netlify.app/) · [공개 개발 코드](https://github.com/Alpenj/DAPIER/tree/main/2ARM_ROBOT) · [양팔 연구 기록](https://github.com/Alpenj/DAPIER/blob/main/2ARM_ROBOT/docs/RESEARCH_SUMMARY_KO.md) · [VSLAM 협업 코드](https://github.com/shouttt1320/Dapier_project_visaul_slam) · [학습 아카이브](../../README.md)

## 프로젝트 목표

초기에는 박스를 열어 신발을 꺼내고 운반하는 과제를 검토했습니다. 이후 물체 인식·조작·정리를 이동 플랫폼과 연결하고, 청소까지 확장하는 가정용 서비스 로봇 방향으로 정리했습니다. 초기 신발 과제는 연구 이력으로 남기되 현재 프로젝트 전체를 그 과제 하나로 설명하지 않습니다.

아래 흐름은 통합 목표입니다. 이동 모듈이나 양팔 실험 하나의 성공으로 전체 실물 과제가 완료됐다고 판단하지 않습니다.

```text
지도 작성·자기위치 추정
          ↓
작업 위치로 이동·도착과 정지 확인
          ↓
물체 관측·접근·집기·결과 확인
          ↓
운반·배치와 후속 서비스 작업
```

## 내 담당과 협업 범위

| 영역 | 수행하는 작업 | 코드와 근거 |
|---|---|---|
| 모방학습 | 시연 데이터 의미·시간 정렬·분할, 행동 묶음과 정책 평가 | [데이터·학습 패키지](https://github.com/Alpenj/DAPIER/tree/main/2ARM_ROBOT/src/shoe_sorting_data) |
| 시뮬레이션 | SO-101·그리퍼·작업공간 모델, 접촉·하중·경로와 실패 분석 | [MuJoCo 모델](https://github.com/Alpenj/DAPIER/tree/main/2ARM_ROBOT/sim/mobile_dual_so101) |
| Sim-to-Real | 관측과 관절 상태·좌표·보정·제한 명령을 연결하는 검증 | [프로젝트 구성과 검증 상태](https://github.com/Alpenj/DAPIER/blob/main/2ARM_ROBOT/README.md) |
| VSLAM 협업 | 팀원 주 담당 모듈의 설계·구현·코드 작업 보조 참여 | [이동·도킹 모듈](https://github.com/shouttt1320/Dapier_project_visaul_slam) |

교육 예제, 외부 라이브러리와 팀원이 주도한 구현은 개인 단독 성과와 구분합니다. DAPIER는 현재 공개 저장소이며, 기존의 접근 권한 필요 안내를 수정했습니다.

## 양팔에서 조사한 문제와 결과

### 접촉 후에도 파지가 풀리는 문제

접촉 여부만 보지 않고 접촉 위치·법선력·집게 간격의 변화를 비교했습니다. 그리퍼 단독 시험과 팔 장착 시험에서 양측 접촉 후의 추가 압축이 달랐고, 동일 상태에서 닫기 조건을 바꿔 파지 유지에 미치는 영향을 조사했습니다. 접촉 형성과 실제 하중 지지는 서로 다른 조건으로 기록했습니다.

### 계획 오차와 실행 오차를 구분한 이유

들기 끝점의 TCP 오차가 0.611845 mm로 기존 0.5 mm 기준을 넘었습니다. 같은 상태에서 계획 FK 잔차와 실행 추종 오차를 나누고, 기존 DLS 계산을 한 번 더 적용한 비교에서는 실행 후 오차가 0.358577 mm로 줄었습니다. 허용 기준을 바꾼 결과가 아니라 특정 시뮬레이션 조건에서 계획 잔차를 줄인 결과입니다.

### 기본 시작 자세부터 유지까지 연결한 후보

2026-09-21 후보에서는 normal HOME부터 접근·집기·들기·3초 HOLD를 하나의 연속 SIM으로 실행했습니다. 기록된 길이는 18,203 physics step / 36.406 s이며 HOLD 구간 자체가 3.000 s입니다. 접근 구간의 copied/live 표본 5,582개와 마지막 적분 상태도 따로 대조했습니다.

이 결과는 [고정 커밋 f6b61db](https://github.com/Alpenj/DAPIER/commit/f6b61dbc81273f6d775d96f7950461fac9113cbb)와 [PR #68](https://github.com/Alpenj/DAPIER/pull/68)에 보존돼 있습니다. **PR은 닫혔지만 병합되지 않았습니다.** 현재 main의 기본 실행기, ACT 정책이나 실물 전체 과제의 성공으로 표시하지 않습니다. 비교 조건·수치·실패 원인과 후속 보정 연구는 [연구 기록](https://github.com/Alpenj/DAPIER/blob/main/2ARM_ROBOT/docs/RESEARCH_SUMMARY_KO.md)에 모았습니다.

## VSLAM·Nav2·도킹의 현재 공개 구현

소스 확인 기준은 **2026-10-08**, revision은 [`3942b81a0d3131aeed6d97fad83c2a5b389ec18a`](https://github.com/shouttt1320/Dapier_project_visaul_slam/tree/3942b81a0d3131aeed6d97fad83c2a5b389ec18a)입니다. 아래는 코드와 문서에서 확인한 구성입니다. 주행·도킹 정확도나 실물 반복 성공률의 측정 결과는 아닙니다.

| 영역 | 공개 소스에서 확인한 내용 | 원문 |
|---|---|---|
| 플랫폼과 센서 | TurtleBot3 Waffle Pi, Ubuntu 24.04·ROS 2 Jazzy, Astra S RGB-D, Raspberry Pi 4와 PC 구성 | [README](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/3942b81a0d3131aeed6d97fad83c2a5b389ec18a/README.md) |
| 지도 기반 위치 추정 | `rtabmap_slam/rtabmap` 노드에 저장 DB를 전달하고 `Mem/IncrementalMemory=false`, `Mem/InitWMWithAllNodes=true`로 localization 구성 | [navigation launch](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/3942b81a0d3131aeed6d97fad83c2a5b389ec18a/robot_ws/src/turtlebot3_visual_slam/launch/vslam_navigation.launch.py) |
| 자율주행 연결 | RTAB-Map의 map 출력, RGB·depth·CameraInfo·IMU·odometry 연결과 Nav2 `navigation_launch.py` 포함 | [navigation launch](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/3942b81a0d3131aeed6d97fad83c2a5b389ec18a/robot_ws/src/turtlebot3_visual_slam/launch/vslam_navigation.launch.py) |
| 정밀 도킹 | 마커 탐색·정렬·접촉 접근 단계와 범퍼 입력을 사용하는 `precision_approacher` 코드, launch 연결 | [precision_approacher_node.py](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/3942b81a0d3131aeed6d97fad83c2a5b389ec18a/robot_ws/src/precision_docker/precision_docker/precision_approacher_node.py) |
| 조작 화면 | `precision_docker`의 docking GUI를 내비게이션과 함께 실행하는 구성 | [navigation launch](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/3942b81a0d3131aeed6d97fad83c2a5b389ec18a/robot_ws/src/turtlebot3_visual_slam/launch/vslam_navigation.launch.py) |

기존 문서는 9월 7일의 다른 revision을 기준으로 RTAB-Map localization 부재를 설명했습니다. 위 revision에서는 해당 노드가 실제 launch에 있으므로 그 설명을 현재 상태에 적용하지 않습니다. 현재는 **RGB-D 매핑·localization·Nav2·정밀 도킹 코드가 존재하며 현장 통합·재현은 별도 확인하는 모듈**로 소개합니다.

정밀 도킹의 접촉 판정과 실제 전기적 충전 성공도 같은 결과가 아닙니다. 코드에 범퍼 입력이나 도킹 완료 상태가 있다는 이유만으로 충전 성공을 주장하지 않습니다.

## 이동과 양팔을 연결할 지점

| 연결 경계 | 통합에서 확인할 내용 |
|---|---|
| 위치 추정 → 작업 좌표 | map·odom·base·카메라·양팔 좌표계와 관측 시각, 위치 추정 품질 |
| 이동 → 조작 시작 | 도착 판정과 실제 베이스 정지, 조작 중 이동 명령 처리 |
| 조작 → 후속 이동 | 파지·과제 결과, 물체 유지 상태와 이동 가능한 팔 자세 |
| 공통 실행 기록 | 같은 시도의 미션 ID, 센서·관절·이동 상태와 실패·중단 원인 |

위 항목은 통합 검증 대상입니다. 두 저장소에 코드가 존재하는 것과 모든 연결이 현재 장비에서 검증된 것은 구분합니다. 작업공간용 RGB-D와 이동용 Astra S, 과거 H201 구성과 이후 OS30A 연구도 해당 날짜·설정·보정에서 각각 확인합니다.

## 다음에 남길 결과

현재 장비에서의 좌표·관절 대응과 제한된 실제 조작, 학습 정책의 보류 평가, 이동·조작의 연속 실행을 각각 기록합니다. 성공 기준뿐 아니라 시작 조건, 시도 수, 실패·중단 사례와 원자료 위치를 함께 남겨야 같은 결과를 다시 판단할 수 있습니다.

공개 설명 갱신: 2026-10-08. 역할은 프로젝트 참여자의 담당 설명을, 구성과 실험 수치는 연결한 소스·기존 실행 기록을 바탕으로 정리했습니다. 이번 문서 갱신에서 로봇·SLAM·정책을 새로 실행하거나 팀원 저장소를 수정하지 않았습니다.
