---
title: "End-to-End Imitation Learning with LeRobot (SO-101)"
date: "November 2025 - Ongoing"
summary: End-to-end imitation learning pipeline on low-cost hardware: custom SO-101 arm, Xbox teleoperation, smartphone vision. Training ACT and Diffusion policies for dexterity tasks.
---

![LeRobot setup](./vellai_kunjan_2.jpg)

# End-to-End Imitation Learning with LeRobot (SO-101)

**Status:** Ongoing | **Stack:** Python, PyTorch, Hugging Face LeRobot, Ubuntu

## Abstract

This project explores the democratization of robotic manipulation by implementing end-to-end imitation learning on low-cost, open-source hardware. Using a custom-fabricated **SO-101 6-DOF manipulator** and the **Hugging Face LeRobot** library, I am developing a pipeline to train policies (ACT, Diffusion) capable of performing dexterity tasks via vision-based teleoperation.

## 1. System Architecture

The system creates a closed-loop imitation learning pipeline. I chose the **SO-101** over the older SO-100 design for its improved structural rigidity and [e.g., cable management, better joint range].

### Hardware Stack

- **Manipulator:** SO-101 6-DOF Arm (custom 3D printed, [PETG/PLA])
- **Actuation:** [e.g., Feetech STS3215] serial bus servos
- **Teleoperation:** Xbox Series X controller (mapped to joint velocity control)
- **Vision:** Smartphone camera via [USB / DroidCam / Wi-Fi] ([X] Hz stream)
- **Compute:** Ubuntu 22.04 [e.g., RTX 3060 or CPU-only]

### Software Stack

- **Framework:** [Hugging Face LeRobot](https://github.com/huggingface/lerobot) (built on PyTorch)
- **Data Format:** LeRobotDataset (Parquet metadata + time-synced MP4)
- **OS:** Ubuntu Linux

## 2. Methodology

### 2.1 Teleoperation & Data Collection

To generate high-quality expert demonstrations, I implemented a leader-follower teleoperation scheme using an Xbox controller.

- **Mapping:** Analog sticks control end-effector delta positions (x, y, z). Triggers control gripper state.
- **Sync:** Images are captured at [30/60] FPS and synchronized with joint state vectors (position, velocity) to minimize drift between observation and action spaces.

### 2.2 Policy Training

I am benchmarking two state-of-the-art imitation learning algorithms:

1. **ACT (Action Chunking with Transformers):** Uses a VAE to encode temporal action sequences.
2. **Diffusion Policy:** Models the action distribution as a denoising process.

Example training configuration:

```yaml
# Example Training Config
training:
  offline_steps: 80000
  batch_size: 64
  eval_freq: 5000
policy:
  type: "act"
  n_action_steps: 100
```

## 3. Preliminary Results & Current Milestones

- **Teleoperation:** Real-time control with latency under [X] ms
- **Dataset:** [X] episodes of pick-and-place (or object pushing) tasks collected
- **Pipeline validation:** Data recording and LeRobotDataset export verified
- **Current challenges:** Tuning PID values on shoulder joints to reduce jitter during the hold phase of collection

## 4. Next Steps

- Complete policy training runs and evaluate on real hardware
- Add quantitative success rates and ablation studies
- Record a short demo video or GIF of teleoperation and policy execution

## References

- [LeRobot on GitHub](https://github.com/huggingface/lerobot)
- [LeRobot Documentation](https://huggingface.co/docs/lerobot)
