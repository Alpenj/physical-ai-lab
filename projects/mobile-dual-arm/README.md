# 이동형 양팔 로봇 — Imitation Learning · Simulation · Sim-to-Real

**전형주 주 담당: 양팔 로봇의 모방학습(Imitation Learning), 시뮬레이션(Simulation), Sim-to-Real.**

Visual SLAM 기반 이동 플랫폼에 SO-101 양팔을 결합해 작업 위치로 이동하고 물체를 조작하는 팀 프로젝트입니다. 저는 양팔 태스크의 학습·시뮬레이션·실물 전이 검증을 중심으로 작업하며, **VSLAM 모듈의 설계·구현·코드 작업에도 협업 참여했습니다.** 이동 모듈과 양팔 태스크를 하나의 작업 흐름으로 연결하는 것이 팀의 통합 목표입니다.

[전형주 포트폴리오](https://julianjeonresume.netlify.app/) · [Workbench](https://julianjeonresume.netlify.app/workbench/) · [VSLAM 협업 코드](https://github.com/shouttt1320/Dapier_project_visaul_slam) · [학습 아카이브로 돌아가기](../../README.md)

## 주 담당 영역

| 영역 | 담당 범위 | 결과를 확인하는 기준 |
|---|---|---|
| Imitation Learning | 양팔 태스크의 모방학습과 시연 데이터·정책 실험 | 데이터 준비, 학습 실행, 정책 평가를 서로 다른 단계로 확인 |
| Simulation | 양팔 로봇과 태스크의 시뮬레이션·실험·검증 | 사용 모델과 실험 조건을 확인하고 가상 결과와 실물 결과를 구분 |
| Sim-to-Real | 시뮬레이션과 실제 장비를 연결하는 적용·검증 작업 | 적용을 위한 준비, 장치별 검증, 실제 태스크 성공을 구분 |

### VSLAM 협업 기여

Visual SLAM·이동 플랫폼은 팀원 `shouttt1320`이 주 담당하며, 저는 설계·구현·코드 작업을 보조하며 함께 개발했습니다. 개인 기여는 **모방학습·시뮬레이션·Sim-to-Real 주 담당 + VSLAM 설계·구현 협업**으로 구분합니다.

담당 범위와 개발 완료 상태는 별도로 관리하며, 세부 구현·실험 결과는 코드 변경 이력과 실행 기록으로 연결합니다. 역할 명확화: 2026-09-07.

## 프로젝트 목표

이동과 조작을 별개의 데모로 끝내지 않고 하나의 작업으로 연결합니다. TurtleBot3 Waffle Pi 기반 플랫폼의 지도 작성·자기위치 추정·목표 지점 이동에 양팔 로봇의 물체 조작을 결합하는 것이 목표입니다. 양팔 프로젝트에서 설정한 구체적인 과제는 박스가 있는 위치까지 이동하고, 박스를 열어 신발을 꺼낸 뒤 운반·배치하는 것입니다.

아래 흐름은 **팀의 통합 목표**이며, 전체 과정을 실물에서 완료했다는 실험 결과가 아닙니다.

```text
환경 관측·지도 작성 / 자기위치 추정
                    ↓
             작업 위치까지 이동
                    ↓
          도착·정지·작업 가능 상태 확인
                    ↓
               양팔 태스크 수행
                    ↓
             결과 확인·운반·배치
```

## 역할과 코드 출처

| 구분 | 담당 범위 | 확인할 자료 |
|---|---|---|
| 전형주 / 주 담당 | Imitation Learning · Simulation · Sim-to-Real을 중심으로 하는 양팔 태스크 작업 | [DAPIER의 2ARM_ROBOT](https://github.com/Alpenj/DAPIER/tree/main/2ARM_ROBOT) — 비공개 저장소, 접근 권한 필요 |
| 전형주 / 협업 기여 | VSLAM 모듈의 설계·구현·코드 작업 보조 참여 | [VSLAM 협업 코드](https://github.com/shouttt1320/Dapier_project_visaul_slam) |
| shouttt1320 / 주 담당 | Visual SLAM·이동 플랫폼 측 개발 | [Dapier_project_visaul_slam](https://github.com/shouttt1320/Dapier_project_visaul_slam) — 팀원 계정의 공개 저장소 |
| 팀 공동 목표 | 위치 추정·이동과 양팔 조작을 연결하는 전체 작업 흐름 | 두 모듈을 연결한 통합 실행·검증 자료는 별도로 확보할 항목 |

## VSLAM 협업 저장소에서 확인한 구성

소스 확인일은 **2026-09-07**, 확인 기준 revision은 [`00b366c5b56485c1439cab72824754ebfc38fee7`](https://github.com/shouttt1320/Dapier_project_visaul_slam/tree/00b366c5b56485c1439cab72824754ebfc38fee7)입니다. 아래는 정적 코드 확인이며, 이번 문서 작성 중 로봇·SLAM·내비게이션을 실행하지 않았습니다.

| 영역 | 소스에서 확인한 내용 | 원문 |
|---|---|---|
| 플랫폼 환경 안내 | Ubuntu 24.04, ROS 2 Jazzy, TurtleBot3 Waffle Pi 안내. 이 문서에는 LiDAR 기반 Cartographer·SLAM Toolbox 실습도 포함 | [README_SLAM.md](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/00b366c5b56485c1439cab72824754ebfc38fee7/README_SLAM.md) |
| RGB-D 매핑 | RTAB-Map에 RGB·depth·CameraInfo·IMU·odometry를 연결하고, point cloud와 RViz를 구성하는 launch | [vslam_rgbd_imu.launch.py](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/00b366c5b56485c1439cab72824754ebfc38fee7/robot_ws/src/turtlebot3_visual_slam/launch/vslam_rgbd_imu.launch.py) |
| 매핑 설정 | RGB·depth 사용, scan 구독 비활성화, 평면 운동 제약과 depth 기반 occupancy grid 생성 설정 | [rtabmap_params.yaml](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/00b366c5b56485c1439cab72824754ebfc38fee7/robot_ws/src/turtlebot3_visual_slam/config/rtabmap_params.yaml) |
| 저장 지도 내비게이션 | depth를 LaserScan으로 변환하고 저장 지도·AMCL을 사용하는 표준 Nav2 bringup을 포함하는 launch | [vslam_navigation.launch.py](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/00b366c5b56485c1439cab72824754ebfc38fee7/robot_ws/src/turtlebot3_visual_slam/launch/vslam_navigation.launch.py) |

### 설명과 실제 launch의 차이

[`2_start_3d_nav.sh`](https://github.com/shouttt1320/Dapier_project_visaul_slam/blob/00b366c5b56485c1439cab72824754ebfc38fee7/2_start_3d_nav.sh)는 RTAB-Map localization을 실행한다고 설명하지만, 실제로 호출하는 `vslam_navigation.launch.py`에는 RTAB-Map localization 노드가 없고 depth→LaserScan과 표준 Nav2 bringup이 구성돼 있습니다.

따라서 현재 포트폴리오에서는 **RGB-D 매핑 경로와 depth 기반 저장 지도 내비게이션 경로가 준비된 VSLAM 협업 모듈**로 소개합니다. 이를 RTAB-Map localization으로만 이동하는 완성 시스템이나, 양팔까지 연결해 검증을 마친 시스템으로 표현하지 않습니다. 실제 현장 실행 구성이 다른 경우 실행 revision·launch·로그로 별도 확인해야 합니다.

## 양팔 프로젝트와 연결할 지점

다음은 **통합 시 확인할 항목**입니다. 현재 두 저장소 사이에 이 인터페이스가 구현·검증됐다는 주장이 아닙니다.

| 연결 경계 | 확인할 내용 |
|---|---|
| 위치 추정 → 작업 좌표 | map·odom·base·카메라·양팔 좌표계의 연결, 시간 기준, 위치 추정 품질 |
| 이동 → 조작 시작 | 목표 도착 판정과 실제 베이스 정지 확인, 조작 중 이동 명령의 처리 |
| 조작 → 후속 이동 | 양팔 태스크의 성공·실패 상태, 물체 유지 상태와 이동 가능한 자세 |
| 공통 실행 기록 | 같은 시도의 미션 ID, 센서·관절·이동 상태, 중단 원인과 결과 |

이 연결을 확인하면 양팔 실험을 독립된 작업대 데모가 아니라 이동형 로봇 시스템의 일부로 설명할 수 있습니다.

## 현재 공개 근거와 남은 검증

VSLAM 협업 코드는 팀원 계정의 공개 저장소와 위 고정 revision에서 확인할 수 있습니다. 개인 주 담당인 양팔 학습·시뮬레이션·Sim-to-Real의 상세 소스는 DAPIER 접근 권한이 필요하며, 모듈별 코드와 결과를 각각 연결합니다.

이번에 확인한 소스만으로는 주행 성공률, 위치 오차, 반복 시험 결과 또는 이동→양팔 조작의 통합 완주를 판단할 수 없습니다. 통합 결과를 추가할 때에는 사용 장비, 코드 revision, 시작·종료 조건, 시도 수, 성공·실패 기준, 영상·로그를 함께 제시합니다.

역할 분담과 협업 기여는 프로젝트 참여자의 담당 설명을, 모듈 구성은 위 소스를 근거로 정리했습니다. 이번 변경은 포트폴리오 문서의 역할 표기 수정이며, VSLAM 저장소나 로봇 실행 코드를 변경하지 않았습니다.
