# QUB Humanoid

![Ubuntu 22.04](https://img.shields.io/badge/Ubuntu_22.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![C++17](https://img.shields.io/badge/C%2B%2B17-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Isaac Gym](https://img.shields.io/badge/NVIDIA-Isaac_Gym-76B900?style=for-the-badge&logo=nvidia&logoColor=white)

> A 13-DOF quasi-direct-drive bipedal humanoid developed as an undergraduate robotics project.

![QUB_v1.2](QUB%20v1.2%20image.png)

QUB는 기구 설계, 강화학습 기반 보행 제어, 실시간 모터 제어 및 Sim-to-Real 배포 과정을 하나의 로봇 시스템으로 통합하기 위해 개발한 KUDOS 로봇 동아리 학부 프로젝트입니다.

## Project Status

> **Archived — August 2026**
>
> QUB 개발은 최종 액추에이션과 실제 보행 검증에 이르기 전 중단되었습니다. 그러나 13-DOF 기구 설계, URDF 기반 시뮬레이션, 강화학습 환경 구축과 발산 진단, 실시간 제어기 및 IMU 통합에 이르는 과정을 수행했으며, 각 저장소는 그 과정에서 얻은 설계 판단·시행착오·검증 방법·기술적 교훈을 공개하기 위해 정리했습니다.


## Overview

- **로봇**: QUB v1.2 — 13 DOF bipedal (12 leg + torso_yaw), 머리 · 팔 없음
- **크기 / 무게**: 약 100cm / 약 20kg
- **액추에이터**: Robstride RS02 / RS03 / RS04 (CAN 2.0, 1Mbps)
- **메인 제어기**: Intel NUC 11 (Ubuntu Pro 22.04 + PREEMPT-RT)
- **CAN 인터페이스**: PCAN-M.2 4-channel
- **IMU**: MicroStrain 3DM-CV7-AHRS
- **시뮬레이터**: NVIDIA Isaac Gym (학습)
- **개발 환경**: Python, C++17, Ubuntu 22.04 + PREEMPT-RT

무릎의 4-bar linkage와 발목의 병렬 메커니즘은 일반적인 URDF의 closed-loop 제약 한계 때문에 등가 단일 회전 관절로 단순화했습니다.

## Explore the Project
이 저장소는 QUB의 설계·구현·진단 과정과 기술적 교훈을 연결하는 프로젝트 진입점이며, 영역별로 하기 내용들처럼 분리된 레포지토리에 기술하였습니다.


| Repository | Focus | Status |
|---|---|---|
| [QUB_URDF](https://github.com/jaebin401/QUB_URDF) | URDF, meshes and robot description | Archived |
| [QUB_RL](https://github.com/jaebin401/QUB_RL) | `humanoid-gym` 기반 RL v1 | Archived / Reference |
| [QUB_RL_v2](https://github.com/jaebin401/QUB_RL_v2) | `tron1-rl-isaacgym` 기반 RL 환경 및 안정화 실험 | Archived |
| [QUB_Controller](https://github.com/jaebin401/QUB_Controller) | 실시간 C++ 제어, CAN 및 IMU 통합 | Archived |
| [Robstride-Study](https://github.com/jaebin401/Robstride-Study) | RobStride CAN 프로토콜 학습 및 초기 실험 | Reference |

각 레포의 상세 내용과 진행 기록은 해당 레포의 README를 참고해 주세요.

## Validation Status

| 영역 | 결과 | 상태 |
|---|---|---|
| 13-DOF 기구 설계 | QUB v1.2 전체 구조 및 관절 메커니즘 설계 | 완료 |
| URDF 및 시뮬레이션 | Isaac Gym import 및 동역학 실험 | 완료 |
| RL walking | v1·v2 환경 구성 및 발산 원인 분석 | 미완료 |
| 실시간 모터 제어기 | 4채널·500Hz 구조 및 RobStride 프로토콜 구현 | 구현 완료, 전체 실기 검증 미완료 |
| IMU 통합 | MicroStrain CV7-AHRS 데이터 수신 및 자세 변화 확인 | 실기 검증 완료 |
| 전체 모터 연결 | 13개 중 3개 응답 확인 | 미완료 |
| ONNX 정책 통합 | 50Hz policy thread 설계 | 계획 단계 |
| Sim-to-Real 보행 | 실제 하드웨어 walking | 미도출 |


URDF 기반 시뮬레이션, RL 환경 구성, 실시간 제어기의 기반 구조와 CV7-AHRS 통합까지 구현했습니다. 안정적인 walking policy, ONNX 정책 통합 및 실제 하드웨어 보행은 완료하지 못했습니다.


## Hardware Validation and Final Blocker

2026년 7월 현장 테스트에서 CV7-AHRS의 quaternion, angular rate 및 acceleration 데이터 수신을 실제 NUC 환경에서 확인했습니다.

반면 CAN 연결 검사에서는 `can0: ID 2`, `can1: ID 1`, `can2: ID 1`만 응답했고 `can3`에서는 응답이 없었습니다. 설계된 채널-ID 매핑과 실제 배선이 일치하지 않아 이후의 액추에이션 테스트를 중단했습니다.

> 전체 13개 모터의 연결, 방향, joint limit, PD gain 및 비상정지 체계가 검증되지 않았으므로 실제 보행 테스트는 수행하지 않았습니다.


## Team

본 프로젝트는 두 단계로 진행되어 왔으며, 각 단계마다 팀 구성이 달라졌습니다.

### Phase 1 — 하드웨어 설계 (2명)
- **Jaebin Ahn** (본인) — 프로젝트 총괄, 기구 설계, URDF 작업, 시뮬레이션 검증

### Phase 2 — 배선 · 제어 · 강화학습 (6명)
- **Jaebin Ahn** (본인) — 프로젝트 총괄, RL 학습 (Isaac Gym), C++ 실시간 제어기 설계 및 구현, sim-to-real 파이프라인, 리포지토리 관리 및 문서화
- **김정환** — QUB 하드웨어 제작 수정 및 URDF 제작
- **김현기** — 강화학습
- **안희찬** — 강화학습
- **이윤재** — 강화학습
- **황준모** — Isaac Gym 기반 보행 RL 학습 및 발산 문제 해결, 검증용 MuJoCo C++ 제어기 설계 및 Sim-to-Sim 연동 테스트


## Author and Project Lead

**Jaebin Ahn (jaebin401)**  
학부 기계공학 전공 / 소프트웨어 부전공  
KUDOS 로봇 동아리 · Apple Developer Academy

목표: 로봇 연구원. 학부 마치고 대학원 진학 계획.

- GitHub: [@jaebin401](https://github.com/jaebin401)
- Instagram: [통학하는 공대생](https://www.instagram.com/study_4_machine/)
- LinkedIn: [Jaebin Ahn](https://www.linkedin.com/in/jaebin-272ba8366)


## Acknowledgments

본 프로젝트는 다음 오픈소스 작업들에 기반하고 있습니다.

- [Robstride_Control](https://github.com/Seeed-Projects/RobStride_Control) - seeed studio
- [Isaac Gym](https://developer.nvidia.com/isaac-gym) — NVIDIA
- [legged_gym](https://github.com/leggedrobotics/legged_gym) — ETH Zurich Robotic Systems Lab
- [rsl_rl](https://github.com/leggedrobotics/rsl_rl) — ETH Zurich Robotic Systems Lab
- [humanoid-gym](https://github.com/roboterax/humanoid-gym) — Robot Era / Tsinghua / Shanghai Qi Zhi Institute
- [tron1-rl-isaacgym](https://github.com/limxdynamics/tron1-rl-isaacgym) — LimX Dynamics

<br>

> 프로젝트를 지도하고 자원을 지원해주신 조백규 교수님과 기술적인 조언을 제공해주신 RCLab 휴머노이드 분야 석박사과정생 분들께 감사드립니다.
