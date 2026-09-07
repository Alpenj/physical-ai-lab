# Physical AI Lab | 전형주

**모방학습·시뮬레이션·Sim-to-Real을 중심으로 양팔 로봇의 학습과 검증을 기록합니다.**

[포트폴리오·이력서](https://julianjeonresume.netlify.app/) · [GitHub](https://github.com/Alpenj) · [전체 글](articles/)

이 저장소는 완성된 로봇 제품이나 성능 벤치마크가 아니라, Physical AI 교육을 따라가며 개념을 정리하고 확인 범위를 남기는 공개 아카이브입니다. 수업에서 이해한 내용, 코드에서 확인한 내용, 실제 실험 결과와 다음 검증 과제를 구분합니다.

## 처음 방문했다면

| 확인하려는 내용 | 시작 위치 |
|---|---|
| 경력과 프로젝트 전체 맥락 | [Physical AI Portfolio](https://julianjeonresume.netlify.app/) |
| 주 담당 분야와 이동형 양팔 팀 프로젝트 | [이동형 양팔 로봇 — Imitation Learning · Simulation · Sim-to-Real](projects/mobile-dual-arm/README.md) — 주 담당 분야·VSLAM 협업 기여·통합 목표 |
| 데이터와 검증을 바라보는 방식 | [Episode 데이터 계약](articles/2026-09-01-robot-episode-data-contract.html), [시뮬레이션 가정과 검증 범위](articles/2026-09-03-simulation-assumption-range-check.html) |
| 로봇 시스템의 기본 개념 | [로봇 모델·FK·IK](articles/2026-08-06-robot-model-fk-ik-check.html), [ROS 2 통신 계약](articles/2026-08-13-ros2-communication-contract.html) |
| 공개 개발 코드 | [soccerhelper](https://github.com/Alpenj/soccerhelper) — 웹·모바일 팀 운영 MVP |
| 교육용 원본을 따라 읽는 코드 | [SO-101 학습 포크](https://github.com/Alpenj/so101_imitation_learning), [deepThinkCar 학습 저장소](https://github.com/Alpenj/deepThinkCar_mini) |

**저장소의 역할:** DAPIER는 내 수업·개인 실습 코드를 정리하는 작업 저장소이며, 이 저장소는 읽기 쉬운 공개 학습 글을 관리합니다. DAPIER는 2026-09-05 확인 기준 비공개이므로, 해당 링크만으로 외부 검토자가 코드를 볼 수 있다고 안내하지 않습니다. 교육용 포크의 원본 구현은 내 독자 개발 성과와 구분합니다.

## 팀 프로젝트 — 이동형 양팔 로봇

**전형주 주 담당: Imitation Learning · Simulation · Sim-to-Real.**

Visual SLAM으로 위치를 파악하는 TurtleBot3 Waffle Pi 기반 이동 플랫폼에 SO-101 양팔을 결합해, 작업 위치로 이동하고 물체를 조작하는 것이 팀 프로젝트의 목표입니다. 저는 양팔 태스크의 모방학습·시뮬레이션·실물 전이 검증을 중심으로 작업합니다.

**협업 기여: VSLAM 모듈의 설계·구현·코드 작업에도 보조적으로 참여했습니다.** Visual SLAM·이동 플랫폼의 주 담당은 팀원 `shouttt1320`이며, 이동 모듈과 양팔 태스크를 하나의 작업 흐름으로 연결하는 것이 공동 목표입니다. 개별 모듈의 구현과 전체 실물 태스크 성공은 구분합니다.

[주 담당 영역·협업 기여·통합 과제](projects/mobile-dual-arm/README.md) · [VSLAM 협업 코드](https://github.com/shouttt1320/Dapier_project_visaul_slam)

## 전체 글 — 기초에서 검증까지

아래 10개 글은 현재 추적 중인 HTML 전체입니다. GitHub에서는 소스로 보이며, 웹 화면은 로컬 미리보기로 확인할 수 있습니다.

| 순서 | 날짜 | 주제와 문서 |
|---|---|---|
| 01 | 2026-08-04 | [Physical AI 첫 단계](articles/2026-08-04-physical-ai-first-steps.html) |
| 02 | 2026-08-06 | [로봇 모델과 FK·IK 확인](articles/2026-08-06-robot-model-fk-ik-check.html) |
| 03 | 2026-08-11 | [위치·방향 추정, 추적, SLAM](articles/2026-08-11-pose-tracking-slam-state.html) |
| 04 | 2026-08-13 | [ROS 2 통신 계약](articles/2026-08-13-ros2-communication-contract.html) |
| 05 | 2026-08-18 | [피드백과 PID 튜닝](articles/2026-08-18-feedback-pid-tuning-check.html) |
| 06 | 2026-08-20 | [전체 경로·궤적·안전 확인](articles/2026-08-20-global-path-trajectory-safety-check.html) |
| 07 | 2026-08-25 | [로컬 경로와 안전 정지](articles/2026-08-25-local-planning-stop-safety.html) |
| 08 | 2026-08-27 | [작업공간·집기 접근·충돌 검사](articles/2026-08-27-manipulation-reachability-collision.html) |
| 09 | 2026-09-01 | [Episode 데이터 계약](articles/2026-09-01-robot-episode-data-contract.html) |
| 10 | 2026-09-03 | [시뮬레이션 가정과 검증 범위](articles/2026-09-03-simulation-assumption-range-check.html) |

## 파일과 폴더

| 경로 | 역할 |
|---|---|
| [`index.html`](index.html) | 프로필, 최근 글, 관련 영상, 학습 순서를 묶는 아카이브 첫 화면 |
| [`styles.css`](styles.css) | 첫 화면과 글의 공통 스타일 |
| [`articles/`](articles/) | 날짜·주제별 본문 HTML과 문서 안내 |
| [`projects/mobile-dual-arm/`](projects/mobile-dual-arm/README.md) | 이동형 양팔 팀 프로젝트의 주 담당 분야·협업 기여·소스 근거·통합 과제 |
| [`assets/`](assets/) | 본문 그림·도식·이미지 자산; 파일이 있다는 사실을 실험 성공의 증거로 사용하지 않음 |
| [`data/blog-inventory.csv`](data/blog-inventory.csv) | 글 목록 관리 자료 |
| [`data/content-lineage.csv`](data/content-lineage.csv) | 콘텐츠 계보 관리 자료 |

웹 경로와 기존 자료의 연결을 유지하기 위해 글·이미지 파일을 임의로 이동하거나 삭제하지 않습니다. 새 글은 `articles/YYYY-MM-DD-topic.html` 형식으로 추가하고 첫 화면과 글 목록을 함께 갱신합니다.

## 로컬 미리보기

별도의 패키지 설치나 빌드 도구 없이 정적 파일로 확인합니다. 저장소를 받은 폴더에서 실행합니다.

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

브라우저에서 `http://127.0.0.1:8000/`을 엽니다. 종료는 `Ctrl+C`입니다. `index.html`을 직접 열 수도 있습니다.

GitHub Pages용 정적 구조로 준비된 저장소입니다. 실제 호스팅 여부나 배포 성공을 README의 존재만으로 판단하지 않습니다. 위 Netlify 포트폴리오는 별도 사이트입니다.

## 기록과 공개 기준

각 글은 **이해한 개념 → 확인한 코드·자료 → 아직 검증하지 않은 조건 → 다음 실험 질문**으로 읽습니다. 강의 요약, simulation, mock, 실물 결과를 같은 성과로 합치지 않습니다. 숫자 결과를 추가할 때에는 실행 조건·revision·명령·출력물·실패 사례를 함께 제시합니다.

공개 글에는 사적인 Notion 링크, 원시 녹취, 장치 serial, 로컬 경로, 인증 정보 또는 타인의 개인정보를 넣지 않습니다. 이미 공개된 자료도 출처와 사용 범위를 확인하며, 검토하지 않은 전체 파일에 대해 보안 검사가 완료됐다고 주장하지 않습니다.

문서·목록 점검: 2026-09-05. 팀 프로젝트 구조·소스 안내 및 주 담당 분야·VSLAM 협업 기여 명확화: 2026-09-07. 학습 글의 내용 확인과 프로그램·실물의 실행 검증은 별도입니다.
