# QUB : Quasi-directive-drive actuator Used Bipedal robot

> 13 DOF 청소년 크기 휴머노이드 로봇 **QUB v1.2**의 설계부터 강화학습 기반 보행 제어, 그리고 실제 하드웨어 배포까지의 통합 기록.

KUDOS 로봇 동아리에서 진행 중인 학부 연구 프로젝트로, Sim-to-Real RL locomotion을 목표로 합니다. 본 레포지토리는 프로젝트 전반의 진입점이자 하위 레포들을 묶는 우산(umbrella) 역할입니다.

---

## 프로젝트 개요

- **로봇**: QUB v1.2 — 13 DOF bipedal (12 leg + torso_yaw), 머리 · 팔 없음
- **크기 / 무게**: 약 100cm / 약 20kg
- **액추에이터**: Robstride RS02 / RS03 / RS04 (CAN 2.0, 1Mbps)
- **메인 제어기**: Intel NUC 11 (Ubuntu Pro 22.04 + PREEMPT-RT)
- **CAN 인터페이스**: PCAN-M.2 4-channel
- **IMU**: MicroStrain 3DM-CV7-AHRS
- **시뮬레이터**: NVIDIA Isaac Gym (학습) / MuJoCo (sim-to-sim 검증)
- **개발 환경**: Python, C++, Ubuntu 22.04

---

## 하위 레포지토리

| 레포 | 설명 | 베이스 오픈소스 |
|---|---|---|
| [QUB_URDF](https://github.com/jaebin401/QUB_URDF) | 로봇 형상 정보 (URDF + mesh) | — |
| [QUB_RL](https://github.com/jaebin401/QUB_RL) | RL 학습 v1 (frozen, 참조용) | [humanoid-gym](https://github.com/roboterax/humanoid-gym) |
| [QUB_RL_v2](#) | RL 학습 v2 (active development) | [tron1-rl-isaacgym](https://github.com/limxdynamics/tron1-rl-isaacgym) |
| [QUB_Controller](#) | 실시간 C++ 하위 제어기 | — |
| [Robstride-Study](https://github.com/jaebin401/Robstride-Study) | Robstride 액추에이터 제어 스터디 | [Robstride_Control](https://github.com/Seeed-Projects/RobStride_Control)| 

각 레포의 상세 내용과 진행 기록은 해당 레포의 README를 참고해 주세요.

---

## 시스템 흐름

```
QUB_URDF → QUB_RL_tron1 → ONNX → QUB_Controller → CAN bus → QUB v1.2
```

학습 측은 URDF로부터 시뮬레이션 환경을 구성해 정책을 학습하고, 배포 측은 학습된 정책(.onnx)을 실시간 C++ 제어기로 추론하여 모터를 제어합니다.

---

## 팀

본 프로젝트는 두 단계로 진행되어 왔으며, 각 단계마다 팀 구성이 달라졌습니다.

### Phase 1 — 하드웨어 설계 (2명)
- **Jaebin Ahn** (본인) — 프로젝트 총괄, 기구 설계, URDF 작업, 시뮬레이션 검증
- **[]** — 기구 설계

### Phase 2 — 배선 · 제어 · 강화학습 (6명)
- **Jaebin Ahn** (본인) — 프로젝트 총괄, RL 학습 (Isaac Gym), C++ 실시간 제어기 설계 및 구현, sim-to-real 파이프라인
- **[ ]** — 
- **[ ]** — 
- **[ ]** — 
- **[ ]** — 
- **[ ]** — 

모든 단계에서 본인이 시스템 설계 및 핵심 구현을 담당했으며, 함께 해주신 팀원분들께 감사드립니다.

---

## 작성자

**Jaebin Ahn (jaebin401)**  
학부 기계공학 전공 / 소프트웨어 부전공  
KUDOS 로봇 동아리 · Apple Developer Academy

목표: 로봇 연구원. 학부 마치고 대학원 진학 계획.

- GitHub: [@jaebin401](https://github.com/jaebin401)
- Instagram: [통학하는 공대생](https://www.instagram.com/study_4_machine/)
- LinkedIn: [Jaebin Ahn](https://www.linkedin.com/in/jaebin-272ba8366)

---

## 📝 라이선스

본 프로젝트는 학부 연구 목적으로 진행되며, 각 하위 레포의 라이선스를 따릅니다. 자세한 사항은 각 하위 레포의 `LICENSE` 파일을 참조해 주세요.

---

## Acknowledgments

본 프로젝트는 다음 오픈소스 작업들에 기반하고 있습니다.

- [Robstride_Control](https://github.com/Seeed-Projects/RobStride_Contro - seeed studio
- [Isaac Gym](https://developer.nvidia.com/isaac-gym) — NVIDIA
- [legged_gym](https://github.com/leggedrobotics/legged_gym) — ETH Zurich Robotic Systems Lab
- [rsl_rl](https://github.com/leggedrobotics/rsl_rl) — ETH Zurich Robotic Systems Lab
- [humanoid-gym](https://github.com/roboterax/humanoid-gym) — Robot Era / Tsinghua / Shanghai Qi Zhi Institute
- [tron1-rl-isaacgym](https://github.com/limxdynamics/tron1-rl-isaacgym) — LimX Dynamics

또한 적극적으로 도움 주신 RCLab휴머노이드 분야의 석사 멘토분들, 
그리고 누구보다 성심껏 지도 해 주시고, 자원들을 제공 해 주신 조백규 교수님께 감사드립니다.
