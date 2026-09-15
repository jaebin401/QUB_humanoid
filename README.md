# QUB Humanoid

🇰🇷 [Read the Korean version here.](https://github.com/jaebin401/QUB_humanoid/tree/main-KR)

![Ubuntu 22.04](https://img.shields.io/badge/Ubuntu_22.04-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![C++17](https://img.shields.io/badge/C%2B%2B17-00599C?style=for-the-badge&logo=cplusplus&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Isaac Gym](https://img.shields.io/badge/NVIDIA-Isaac_Gym-76B900?style=for-the-badge&logo=nvidia&logoColor=white)

> A 13-DOF quasi-direct-drive bipedal humanoid developed as an undergraduate robotics project.

![QUB_v1.2](QUB%20v1.2%20image.png)

QUB is an undergraduate project developed by the KUDOS Robotics Club to integrate mechanical design, reinforcement-learning-based locomotion, real-time motor control, and Sim-to-Real deployment into a single robotic system.

## Project Status

> **Archived — August 2026**
>
> Development of QUB was discontinued before final actuation and physical walking validation. Nevertheless, the project covered 13-DOF mechanical design, URDF-based simulation, reinforcement learning environment development and divergence diagnosis, real-time control, and IMU integration. Each repository is organized to share the design decisions, failed approaches, validation methods, and technical lessons learned throughout the process.


## Overview

- **Robot**: QUB v1.2 — 13-DOF biped (12 leg joints + `torso_yaw`), without arms or a head
- **Height / mass**: Approximately 100cm / 20kg
- **Actuators**: RobStride RS02 / RS03 / RS04 (CAN 2.0, 1Mbps)
- **Main computer**: Intel NUC 11 (Ubuntu Pro 22.04 + PREEMPT-RT)
- **CAN interface**: PEAK PCAN-M.2, 4 channels
- **IMU**: MicroStrain 3DM-CV7-AHRS
- **Simulator**: NVIDIA Isaac Gym for reinforcement learning
- **Development environment**: Python, C++17, Ubuntu 22.04 + PREEMPT-RT

Because standard URDF does not directly support closed-loop kinematic chains, the knee four-bar linkage and parallel ankle mechanism were modeled as equivalent single revolute joints.

## Explore the Project
This repository serves as the entry point for QUB's design, implementation, diagnostics, and technical lessons. Detailed work is documented in the repositories below, separated by engineering domain.


| Repository | Focus | Status |
|---|---|---|
| [QUB_URDF](https://github.com/jaebin401/QUB_URDF) | URDF, meshes, and robot description | Archived |
| [QUB_RL](https://github.com/jaebin401/QUB_RL) | RL v1 based on `humanoid-gym` | Archived / Reference |
| [QUB_RL_v2](https://github.com/jaebin401/QUB_RL_v2) | RL environment and stability experiments based on `tron1-rl-isaacgym` | Archived |
| [QUB_Controller](https://github.com/jaebin401/QUB_Controller) | Real-time C++ control, CAN, and IMU integration | Archived |
| [Robstride-Study](https://github.com/jaebin401/Robstride-Study) | RobStride CAN protocol study and early experiments | Reference |

See each repository's README for implementation details and development records.

## Validation Status

| Area | Result | Status |
|---|---|---|
| 13-DOF mechanical design | Complete QUB v1.2 structure and joint mechanisms | Completed |
| URDF and simulation | Isaac Gym import and dynamics experiments | Completed |
| RL walking | v1 and v2 environments, including divergence analysis | Incomplete |
| Real-time motor controller | Four-channel 500Hz architecture and RobStride protocol | Implemented; full hardware validation incomplete |
| IMU integration | MicroStrain CV7-AHRS data acquisition and orientation response | Validated on hardware |
| Full motor connectivity | Responses confirmed from 3 of 13 motors | Incomplete |
| ONNX policy integration | 50Hz policy thread design | Planned |
| Sim-to-Real walking | Walking on physical hardware | Not achieved |


The project reached URDF-based simulation, RL environment development, the core real-time controller architecture, and CV7-AHRS integration. A stable walking policy, ONNX policy integration, and physical hardware walking were not completed.


## Hardware Validation and Final Blocker

During on-site testing in July 2026, quaternion, angular-rate, and acceleration data from the CV7-AHRS were successfully received and verified on the target Intel NUC.

The CAN connectivity test, however, received responses only from `can0: ID 2`, `can1: ID 1`, and `can2: ID 1`, with no response on `can3`. Because the physical wiring did not match the intended channel-to-ID mapping, further actuation tests were stopped.

> Physical walking tests were not attempted because connectivity, joint directions, joint limits, PD gains, and the emergency-stop system had not been validated across all 13 motors.


## Team

The project proceeded in two phases with different team structures.

### Phase 1 — Hardware Design

- **Jaebin Ahn** — Project lead, mechanical design, URDF development, and simulation validation

### Phase 2 — Wiring, Control, and Reinforcement Learning

- **Jaebin Ahn** — Project lead, RL training in Isaac Gym, real-time C++ controller design and implementation, Sim-to-Real pipeline, repository management, and documentation
- **김정환** — QUB hardware modifications and URDF development
- **김현기** — Reinforcement learning
- **안희찬** — Reinforcement learning
- **이윤재** — Reinforcement learning
- **황준모** — Isaac Gym locomotion training and divergence debugging, MuJoCo C++ validation controller, and Sim-to-Sim integration testing


## Author and Project Lead

**Jaebin Ahn (jaebin401)**<br>
Undergraduate student in Mechanical Engineering with a minor in Software<br>
KUDOS Robotics Club · Apple Developer Academy @ POSTECH

Goal: robotics researcher. Planning to pursue graduate studies in robotics after completing my undergraduate degree.

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
