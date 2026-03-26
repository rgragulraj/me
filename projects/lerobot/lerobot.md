---
title: "Imitation Learning with LeRobot (SO-101)"
date: "November 2025 - Ongoing"
summary: End-to-end imitation learning on a low-cost SO-101 platform using LeRobot and ACT, with closed-loop deployment for precision pick-and-place tasks.
---

<div class="lerobot-carousel" data-carousel-index="0" style="position: relative; display: flex; align-items: center; gap: 0.75rem; width: 100%; max-width: 100%; margin: 1rem 0;">
  <button type="button" aria-label="Previous" onclick="var c=this.parentNode;var s=c.querySelectorAll('.lerobot-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)-1+2)%2;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});" style="flex-shrink: 0; width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); background: rgba(255,255,255,0.1); color: #fff; font-size: 1.25rem; cursor: pointer; display: flex; align-items: center; justify-content: center;">‹</button>
  <div style="flex: 1; width: 100%; min-width: 0; height: 560px; background: rgba(255,255,255,0.06); border-radius: 8px; overflow: hidden; position: relative;">
    <div class="lerobot-slide" style="width:100%;height:100%;position:absolute;inset:0;"><iframe src="https://www.youtube.com/embed/Q7Np9ZYO1us?autoplay=1&mute=1&playsinline=1" title="Imitation Learning with LeRobot (SO-101) – Video 1" style="width:100%;height:100%;border:none;border-radius:8px;" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
    <div class="lerobot-slide" style="width:100%;height:100%;position:absolute;inset:0;display:none;"><iframe src="https://www.youtube.com/embed/hCE5Kk9XL3o?autoplay=1&mute=1&playsinline=1" title="Imitation Learning with LeRobot (SO-101) – Video 2" style="width:100%;height:100%;border:none;border-radius:8px;" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
  </div>
  <button type="button" aria-label="Next" onclick="var c=this.parentNode;var s=c.querySelectorAll('.lerobot-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)+1)%2;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});" style="flex-shrink: 0; width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); background: rgba(255,255,255,0.1); color: #fff; font-size: 1.25rem; cursor: pointer; display: flex; align-items: center; justify-content: center;">›</button>
</div>

## Tech Stack / Platform

Python / PyTorch · Hugging Face LeRobot · Ubuntu · SO-101 6-DOF Arm

## Abstract

This project implements the ACT (Action Chunking with Transformers) policy using the Hugging Face LeRobot framework on the SO-101 robotic arm. An overhead Logitech C920 webcam serves as the visual input. Demonstrations were collected via teleoperation using a leader arm, and the trained policy is deployed closed-loop on the follower arm.

---

## Content

### Architecture

Closed-loop imitation learning using ACT: collect demonstrations -> train policy -> deploy on robot.

### Hardware

- SO-101 Leader and Follower Arm ([SO-ARM100 / SO-101](https://github.com/TheRobotStudio/SO-ARM100))
- Logitech C920 Webcam

### Software

- Hugging Face LeRobot (PyTorch)
- Ubuntu

### Teleoperation & Data Collection

Keyboard and Xbox controller teleoperation were attempted first, but both were too imprecise for fine manipulation tasks. The workflow then moved to a leader-arm teleoperation setup, which was more natural and produced better demonstrations, but precise placement remained difficult at sub-centimeter scales.

### Policy Training

The model was trained using the ACT policy (Action Chunking with Transformers). Reference paper: [ACT: Learning Fine-Grained Bimanual Manipulation with Low-Cost Hardware](https://arxiv.org/abs/2304.13705). No other policies were evaluated in this phase.

---

## Conclusion / Insights / Future Work

The policy demonstrates that closed-loop imitation learning on low-cost hardware is feasible, but precision is the central limitation. The target task requires placing a block into a shape-matched slot with less than 3 mm tolerance, which exposes two compounding bottlenecks: teleoperated human demonstrations are not consistently precise enough for high-accuracy insertion tasks, and the policy currently has no explicit mechanism to reason about uncertainty before committing to an action.

The next stage of this project will prioritize methods that directly improve reliability on precision-heavy manipulation:

1. **Better data collection for precision tasks**  
Human teleoperation is useful for bootstrapping behavior, but it is not ideal for generating consistently high-precision trajectories. A more reliable data pipeline is to use inverse kinematics with an OpenCV-guided script to execute programmatic pick-and-place motions and log clean demonstrations. This should reduce label noise, improve temporal consistency, and provide stronger supervision for tight-tolerance insertion.

2. **Uncertainty estimation in ACT**  
The current ACT setup predicts actions without an explicit confidence signal. Adding an uncertainty estimation module to the ACT source would allow the controller to detect low-confidence states and trigger a retry or corrective subroutine rather than executing a likely failure action. This is especially important near contact-rich phases such as final alignment and insertion.

3. **Ensemble of policies**  
A single policy can produce high variance on edge cases. Training multiple ACT models with different random seeds or dataset splits, then combining their outputs with a voting or confidence-weighted fusion mechanism, can reduce variance and improve robustness on difficult placements.

4. **Shape-aware visual features**  
The current perception stack can be strengthened by adding DINOv2-based shape-aware features so the policy better distinguishes object-slot geometry. Improved shape encoding should help disambiguate visually similar scenes and produce more accurate alignment actions for insertion.

5. **Language conditioning**  
Integrating CLIP or a comparable vision-language model would allow task instructions in natural language (for example, "pick up the star-shaped block and place it in the star slot"). This would make the policy interface more flexible and improve compositional task specification without rewriting control code for each object type.

6. **Shape and spatial augmentation**  
During training, artificial variation in object shape, position, and orientation can force the policy to learn more position-invariant and orientation-robust behaviors. This kind of augmentation is a practical way to improve generalization and reduce brittle overfitting to a narrow workspace configuration.

Future work will focus specifically on precision-intensive and orientation-intensive manipulation tasks, where sub-millimeter accuracy and object orientation both matter, since these remain the hardest open problems for imitation learning on low-cost robotic arms.

## Resources

- [LeRobot](https://huggingface.co/lerobot)
- [LeRobot (GitHub)](https://github.com/huggingface/lerobot)
- [SO-ARM100 / SO-101](https://github.com/TheRobotStudio/SO-ARM100)
