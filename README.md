# QUB Humanoid

🇰🇷 [Read the Korean version here.](https://github.com/jaebin401/QUB_humanoid/tree/main-KR)

![Ubuntu 22.04](https://img.shields.io/badge/Ubuntu_22.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![C++17](https://img.shields.io/badge/C%2B%2B17-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Isaac Gym](https://img.shields.io/badge/NVIDIA-Isaac_Gym-76B900?style=for-the-badge&logo=nvidia&logoColor=white)

> A 13-DOF quasi-direct-drive bipedal humanoid developed as an undergraduate robotics project.

![QUB_v1.2](QUB%20v1.2%20image.png)

QUB is an undergraduate project developed by the KUDOS Robotics Club to combine mechanical design, reinforcement-learning-based locomotion, real-time controller development, and sim-to-real pipeline development in a single robotic platform.

## Overview

- **Robot**: QUB v1.2 — 13-DOF lower-body bipedal platform (12 leg joints + `torso_yaw`)
- **Height / mass**: Approximately 1.0 m / 20 kg
- **Actuators**: RobStride RS02 / RS03 / RS04 (CAN 2.0, 1 Mbps)
- **Main computer**: Intel NUC 11 (Ubuntu 22.04 with a PREEMPT_RT kernel)
- **CAN interface**: PEAK PCAN-M.2, 4 channels
- **IMU**: MicroStrain 3DM-CV7-AHRS
- **Simulator**: NVIDIA Isaac Gym for reinforcement learning
- **Development environment**: Python, C++17, Ubuntu 22.04 + PREEMPT-RT

Because standard URDF does not directly support closed-loop kinematic chains, the knee four-bar linkage and parallel ankle mechanism were modeled as equivalent single revolute joints.

## Key Contributions

- Led the mechanical design, fabrication, and assembly of the 13-DOF platform, including its joint mechanisms and CAD-to-URDF conversion.
- Designed and implemented a C++17 real-time controller architecture for 13 RobStride actuators across four CAN channels, including 500 Hz motor-control threads and MicroStrain 3DM-CV7-AHRS integration.
- Adapted Isaac Gym-based open-source locomotion frameworks to the custom QUB model, ran PPO training experiments, and investigated training divergence and a standing-still local optimum.

## Explore the Project

This repository serves as the entry point for QUB's design, implementation, diagnostics, and technical lessons. Detailed work is documented in the repositories below, separated by engineering domain.


| Repository | Focus | Status |
|---|---|---|
| [QUB_URDF](https://github.com/jaebin401/QUB_URDF) | URDF, meshes, and robot description | Archived |
| [QUB_RL](https://github.com/jaebin401/QUB_RL) | RL v1 based on `humanoid-gym` | Archived / Reference |
| [QUB_RL_v2](https://github.com/jaebin401/QUB_RL_v2) | RL environment and stability experiments based on `tron1-rl-isaacgym` | Archived |
| [QUB_Controller](https://github.com/jaebin401/QUB_Controller) | Real-time C++ control, CAN, and IMU integration | Archived |
| [RobStride CAN Study](https://github.com/jaebin401/Robstrid-CAN_study) | RobStride CAN protocol study and early experiments | Reference |

See each repository's README for implementation details and development records.

## Project Outcome

> **Archived — August 2026**

The formal team project concluded in May 2026, followed by final hardware diagnostics and repository archival through August 2026. The project reached 13-DOF mechanical design, URDF-based simulation, reinforcement learning environment development, real-time controller implementation, and hardware validation of the IMU. Development concluded before full-motor actuation and physical walking validation.

## Validation Status

| Area | Result | Status |
|---|---|---|
| 13-DOF mechanical design | Complete QUB v1.2 structure and joint mechanisms | Completed |
| URDF and simulation | Isaac Gym import and dynamics experiments | Completed |
| RL walking | v1 and v2 environments, including divergence analysis | Incomplete |
| Real-time motor controller | Four-channel 500 Hz architecture and RobStride protocol | Implemented; full hardware validation incomplete |
| IMU integration | MicroStrain CV7-AHRS data acquisition and orientation response | Validated on hardware |
| Full motor connectivity | Responses confirmed from 3 of 13 motors | Incomplete |
| ONNX policy integration | 50 Hz policy thread design | Planned |
| Sim-to-Real walking | Walking on physical hardware | Not achieved |

## Limitations and Final Blocker

During on-site testing in July 2026, quaternion, angular-rate, and acceleration data from the CV7-AHRS were successfully received and verified on the target Intel NUC.

The CAN connectivity test, however, received responses only from `can0: ID 2`, `can1: ID 1`, and `can2: ID 1`, with no response on `can3`. Because the physical wiring did not match the intended channel-to-ID mapping, further actuation tests were stopped.

> Physical walking tests were not attempted because connectivity, joint directions, joint limits, PD gains, and the emergency-stop system had not been validated across all 13 motors.


## Team

The project proceeded in two phases with different team structures.

### Phase 1 — Hardware Design

- **Jaebin Ahn** — Project lead, mechanical design, URDF development, and simulation validation

### Phase 2 — Wiring, Control, and Reinforcement Learning

- **Jaebin Ahn** — Project lead, RL training in Isaac Gym, real-time C++ controller design and implementation, sim-to-real pipeline development, repository management, and documentation
- **Jeonghwan Kim (김정환)** — QUB hardware modifications and URDF development
- **Hyunki Kim (김현기)** — Reinforcement learning
- **Heechan Ahn (안희찬)** — Reinforcement learning
- **Yoonjae Lee (이윤재)** — Reinforcement learning
- **Junmo Hwang (황준모)** — Isaac Gym locomotion training and divergence debugging, MuJoCo C++ validation controller, and Sim-to-Sim integration testing


## Author and Project Lead

**Jaebin Ahn (jaebin401)**<br>
Undergraduate student in Mechanical Engineering with a minor in Software<br>
KUDOS Robotics Club · Apple Developer Academy @ POSTECH

Research interests: legged locomotion, whole-body control, and the integration of model-based and learning-based control.

- GitHub: [@jaebin401](https://github.com/jaebin401)
- Instagram: [@study_4_machine](https://www.instagram.com/study_4_machine/)
- LinkedIn: [Jaebin Ahn](https://www.linkedin.com/in/jaebin-272ba8366)


## Acknowledgments

This project builds upon the following open-source projects and tools.

- [RobStride_Control](https://github.com/Seeed-Projects/RobStride_Control) — Seeed Studio
- [Isaac Gym](https://developer.nvidia.com/isaac-gym) — NVIDIA
- [legged_gym](https://github.com/leggedrobotics/legged_gym) — ETH Zurich Robotic Systems Lab
- [rsl_rl](https://github.com/leggedrobotics/rsl_rl) — ETH Zurich Robotic Systems Lab
- [humanoid-gym](https://github.com/roboterax/humanoid-gym) — Robot Era / Tsinghua / Shanghai Qi Zhi Institute
- [tron1-rl-isaacgym](https://github.com/limxdynamics/tron1-rl-isaacgym) — LimX Dynamics

<br>

> I would like to thank Professor Baek-Kyu Cho for his guidance and support, as well as the graduate researchers in RCLab's humanoid robotics group for their technical advice.
