---
title: "Imitation Learning with LeRobot (SO-101)"
date: "November 2025 - Ongoing"
summary: End-to-end imitation learning pipeline on low-cost hardware: custom SO-101 arm, Xbox teleoperation, smartphone vision. Training ACT and Diffusion policies for dexterity tasks.
---

![LeRobot setup](./vellai_kunjan_2.jpg)

# Imitation Learning with LeRobot (SO-101)

**November 2025 — Ongoing**

## Tech Stack / Platform

Python · Hugging Face LeRobot · Ubuntu · SO-101 6-DOF Arm 

## Abstract

I'm building a full imitation learning pipeline from scratch on low-cost hardware—because I wanted to prove it's possible without a $50K robot. Custom SO-101 arm, Xbox controller for teleoperation, smartphone as the eyes, and LeRobot doing the heavy lifting. The goal: train policies (ACT, Diffusion) that can actually perform dexterity tasks on real hardware.

---

## Content

### Architecture

Closed-loop imitation learning: collect demonstrations → train policy → deploy on robot. I chose the **SO-101** over the older SO-100 for better structural rigidity and cable management—small design choices that matter when you're chasing repeatability.

**Hardware:** Custom 3D-printed SO-101 arm, Feetech serial servos, Xbox Series X controller (joint velocity control), smartphone camera for vision.

**Software:** Hugging Face LeRobot (PyTorch), LeRobotDataset format (Parquet + time-synced MP4). Everything runs on consumer hardware.

### Teleoperation & Data Collection

I built a leader-follower teleop scheme with the Xbox controller. Analog sticks → end-effector delta (x, y, z). Triggers → gripper. Images and joint states are synced at capture time to keep observation and action spaces aligned—that sync is critical, and I spent time getting it right.

### Policy Training

Benchmarking two SOTA algorithms: **ACT** (action chunking with transformers, VAE-encoded temporal sequences) and **Diffusion Policy** (denoising-based action distribution). Config sanity-checked for my hardware constraints (batch size, chunk length, eval frequency).

### Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Shoulder joint jitter during hold phase | Tuning PID values on servos—iterative, but critical for clean demos |
| Vision-action sync drift | Timestamp-based alignment, validated with offline checks |
| Low-cost hardware constraints | LeRobot's efficient data format + careful batch sizing for training |

---

## Insights

This project taught me how to think in pipelines—from raw teleop data to deployable policies—and that data quality trumps quantity every time. I walked away with a solid grasp of imitation learning fundamentals, the patience to debug hardware-software interfaces, and the confidence that I can ship something end-to-end on a shoestring budget. This is groundwork I'll carry into every robotics project from here: understanding the full stack lets me make better choices at each layer. More than that, it's my first step toward combining AI and robotics for autonomy—I see this as the foundation for scaling to more complex tasks, multi-agent setups, and eventually systems that can adapt and generalize. This is where I'm building from.
