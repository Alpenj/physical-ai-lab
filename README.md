# Physical AI Lab | 전형주

**모방학습·시뮬레이션·Sim-to-Real을 중심으로 로봇의 학습과 검증을 기록합니다.**

[포트폴리오·이력서](https://julianjeonresume.netlify.app/) · [공개 개발 코드 DAPIER](https://github.com/Alpenj/DAPIER) · [양팔 프로젝트](projects/mobile-dual-arm/README.md) · [전체 글](articles/)

DAPIER 국비교육에서 배운 개념을 실습과 프로젝트에 적용하며 정리한 공개 학습 아카이브입니다. 코드와 실험 이력은 DAPIER 저장소에, 읽기 쉬운 설명과 프로젝트 안내는 이곳에 둡니다. 교육 예제, 직접 설계·수정한 부분, 팀 협업과 실제 실험 결과를 구분합니다.

## 처음 방문했다면

| 확인하려는 내용 | 시작 위치 |
|---|---|
| 경력과 프로젝트 전체 맥락 | [Physical AI Portfolio](https://julianjeonresume.netlify.app/) |
| 주 담당 분야와 이동형 양팔 팀 프로젝트 | [TJJ — 모방학습·시뮬레이션·Sim-to-Real](projects/mobile-dual-arm/README.md) |
| 파지 실패·위치 오차·미끄러짐을 조사한 과정 | [양팔 조작 연구 기록](https://github.com/Alpenj/DAPIER/blob/main/2ARM_ROBOT/docs/RESEARCH_SUMMARY_KO.md) |
| 실제 개발 코드와 폴더별 실행 안내 | [DAPIER](https://github.com/Alpenj/DAPIER) · [2ARM_ROBOT](https://github.com/Alpenj/DAPIER/tree/main/2ARM_ROBOT) |
| 데이터와 검증을 바라보는 방식 | [Episode 데이터 계약](articles/2026-09-01-robot-episode-data-contract.html), [시뮬레이션 가정과 검증 범위](articles/2026-09-03-simulation-assumption-range-check.html) |
| 로봇 시스템의 기본 개념 | [로봇 모델·FK·IK](articles/2026-08-06-robot-model-fk-ik-check.html), [ROS 2 통신 계약](articles/2026-08-13-ros2-communication-contract.html) |
| 웹·모바일 개발 | [soccerhelper](https://github.com/Alpenj/soccerhelper) — 팀 운영 MVP |
| 교육용 원본을 따라 읽는 코드 | [SO-101 학습 코드](https://github.com/Alpenj/DAPIER/tree/main/so101_imitation_learning), [deepThinkCar 실습](https://github.com/Alpenj/DAPIER/tree/main/deepThinkCar_mini) |

**DAPIER는 현재 공개 저장소입니다.** 과거의 비공개 안내를 수정했으며, 교육용 포크를 통합한 코드는 DAPIER의 해당 하위 폴더로 연결합니다. 외부 원본 구현과 라이브러리는 개인의 독자 개발 성과로 계산하지 않습니다.

## 팀 프로젝트 — TJJ 이동형 양팔 로봇

**주 담당: Imitation Learning · Simulation · Sim-to-Real.**

SO-101 양팔의 물체 조작을 TurtleBot3 Waffle Pi의 이동과 연결하고 있습니다. 초기 박스·신발 정리 실험을 바탕으로 물체 정리와 가정용 서비스 작업으로 범위를 확장했습니다. 청소까지 이어지는 동작은 장기 목표이며, 전체 실물 과제를 완료했다는 의미는 아닙니다.

저는 시연 데이터, 정책 학습, 물리 모델, 접촉·경로 검사와 실물 전이 검증을 중심으로 작업합니다. 파지 압축, 계획 잔차와 실행 추종 오차, 접촉 솔버에 따른 미끄러짐을 비교하고 결과를 고정 소스와 연결해 기록했습니다.

**VSLAM 모듈의 설계·구현·코드 작업에도 협업 참여했습니다.** Visual SLAM·이동 플랫폼의 주 담당은 팀원 `shouttt1320`입니다. 현재 협업 소스에는 RTAB-Map RGB-D 매핑·localization, Nav2, 듀얼 ArUco 도킹과 GUI가 있습니다. 개별 모듈의 코드 구현, 현장 재현과 이동·양팔 조작 통합 성공은 따로 확인합니다.

[담당 범위·현재 소스·통합 과제](projects/mobile-dual-arm/README.md) · [양팔 실험 근거](https://github.com/Alpenj/DAPIER/blob/main/2ARM_ROBOT/docs/RESEARCH_SUMMARY_KO.md) · [VSLAM 협업 코드](https://github.com/shouttt1320/Dapier_project_visaul_slam)

### 실험 결과를 읽을 때

2026-09-21의 후보 커밋에는 기본 시작 자세부터 접근·집기·들기·3초 유지까지 이어진 단일 연속 SIM 결과가 있습니다. [PR #68](https://github.com/Alpenj/DAPIER/pull/68)에 보존된 미병합 연구 결과이므로 현재 `main`의 기본 실행 성능이나 실물 성공으로 소개하지 않습니다. 수치와 비교 조건, 이후 남은 검증은 위 연구 기록에서 확인할 수 있습니다.

## 학습 글 — 기초에서 검증까지

기존에 공개한 학습 글입니다. GitHub에서는 HTML 소스로 보이며, 웹 화면은 로컬 미리보기로 확인할 수 있습니다. 글을 작성한 날짜와 이후의 프로젝트 상태를 구분합니다.

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
| [`index.html`](index.html) | 프로필, 최근 글, 관련 영상과 학습 순서를 묶는 아카이브 첫 화면 |
| [`styles.css`](styles.css) | 첫 화면과 글의 공통 스타일 |
| [`articles/`](articles/) | 날짜·주제별 본문 HTML과 문서 안내 |
| [`projects/mobile-dual-arm/`](projects/mobile-dual-arm/README.md) | 팀 프로젝트의 담당 범위·소스·실험 근거·통합 과제 |
| [`assets/`](assets/) | 본문 그림·도식·이미지 자산 |
| [`data/blog-inventory.csv`](data/blog-inventory.csv) | 글 목록 관리 자료 |
| [`data/content-lineage.csv`](data/content-lineage.csv) | 콘텐츠 계보 관리 자료 |

웹 경로와 기존 자료의 연결을 유지하기 위해 글·이미지 파일을 임의로 이동하거나 삭제하지 않습니다. 새 글은 `articles/YYYY-MM-DD-topic.html` 형식으로 추가하고 첫 화면과 글 목록을 함께 갱신합니다.

## 로컬 미리보기

별도의 패키지 설치나 빌드 도구 없이 정적 파일로 확인합니다. 저장소를 받은 폴더에서 실행합니다.

```bash
python3 -m http.server 8000 --bind 127.0.0.1
```

브라우저에서 `http://127.0.0.1:8000/`을 엽니다. 종료는 `Ctrl+C`입니다. `index.html`을 직접 열 수도 있습니다.

GitHub Pages용 정적 구조로 준비된 저장소입니다. 실제 호스팅 여부나 배포 성공은 별도 확인이 필요합니다. 위 Netlify 포트폴리오는 별도 사이트이며 이 저장소의 문서 수정만으로 해당 사이트가 갱신되지는 않습니다.

## 기록과 공개 기준

각 글은 이해한 개념, 확인한 코드·자료, 관찰 결과와 남은 질문을 연결합니다. 강의 요약, simulation, mock과 실물 결과를 같은 성과로 합치지 않습니다. 숫자 결과에는 실행 조건·revision·입력과 출력·실패 사례를 함께 남깁니다.

공개 글에는 사적인 Notion 링크, 원시 녹취, 장치 serial, 개인 로컬 경로, 인증 정보나 타인의 개인정보를 넣지 않습니다. 외부 자료는 출처와 사용 범위를 유지합니다.

프로젝트 소개·공개 소스 링크 갱신: 2026-10-08. 기존 학습 글 전체의 재검토나 로봇 실험의 재실행을 뜻하지 않습니다.
