---
title: "Imitation Learning with LeRobot (SO-101)"
date: "November 2025 - Ongoing"
summary: End-to-end imitation learning pipeline on low-cost hardware: custom SO-101 arm, Xbox joystick teleoperation, smartphone vision with Droid cam and OpenCV. Training ACT policy for dexterity tasks.
---

<div class="lerobot-carousel" data-carousel-index="0" style="position: relative; display: flex; align-items: center; gap: 0.75rem; max-width: 100%; margin: 1rem 0;">
  <button type="button" aria-label="Previous" onclick="var c=this.parentNode;var s=c.querySelectorAll('.lerobot-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)-1+2)%2;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});" style="flex-shrink: 0; width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); background: rgba(255,255,255,0.1); color: #fff; font-size: 1.25rem; cursor: pointer; display: flex; align-items: center; justify-content: center;">‹</button>
  <div style="flex: 1; aspect-ratio: 16/9; min-height: 200px; background: rgba(255,255,255,0.06); border-radius: 8px; overflow: hidden; position: relative;">
    <div class="lerobot-slide" style="width:100%;height:100%;position:absolute;inset:0;"><iframe src="https://www.youtube.com/embed/Q7Np9ZYO1us" title="Imitation Learning with LeRobot (SO-101) – Video 1" style="width:100%;height:100%;border:none;border-radius:8px;" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
    <div class="lerobot-slide" style="width:100%;height:100%;position:absolute;inset:0;display:none;"><iframe src="https://www.youtube.com/embed/hCE5Kk9XL3o" title="Imitation Learning with LeRobot (SO-101) – Video 2" style="width:100%;height:100%;border:none;border-radius:8px;" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>
  </div>
  <button type="button" aria-label="Next" onclick="var c=this.parentNode;var s=c.querySelectorAll('.lerobot-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)+1)%2;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});" style="flex-shrink: 0; width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); background: rgba(255,255,255,0.1); color: #fff; font-size: 1.25rem; cursor: pointer; display: flex; align-items: center; justify-content: center;">›</button>
</div>

## Tech Stack / Platform

Python · Hugging Face LeRobot · Ubuntu · SO-101 6-DOF Arm 

## Abstract

I'm building a full imitation learning pipeline from scratch on low-cost hardware—because I wanted to prove it's possible without a $50K robot. Custom SO-101 arm, Xbox joystick for teleoperation, Droid cam on my phone and OpenCV on my laptop for visual, and LeRobot doing the heavy lifting. I used ACT policy training for imitation learning and am currently working on building my own policies.

---

## Content

### Architecture

Closed-loop imitation learning: collect demonstrations → train policy → deploy on robot. I chose the **SO-101** over the older SO-100 for better structural rigidity and cable management—small design choices that matter when you're chasing repeatability.

**Hardware:** Custom 3D-printed SO-101 arm, Feetech serial servos, Xbox joystick for teleoperation.

**Software:** Hugging Face LeRobot (PyTorch), LeRobotDataset format (Parquet + time-synced MP4), Droid cam on phone, OpenCV on laptop for visual. Everything runs on consumer hardware.

### Teleoperation & Data Collection

I built a teleoperation setup using an Xbox joystick to train the bot on ACT imitation learning. I used Droid cam on my phone and OpenCV on my laptop for visual. Images and joint states are synced at capture time to keep observation and action spaces aligned—that sync is critical, and I spent time getting it right.

### Policy Training

I only did the ACT policy training (action chunking with transformers, VAE-encoded temporal sequences). I'm currently working on building my own policies. Config sanity-checked for my hardware constraints (batch size, chunk length, eval frequency).

### Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Shoulder joint jitter during hold phase | Tuning PID values on servos—iterative, but critical for clean demos |
| Vision-action sync drift | Timestamp-based alignment, validated with offline checks |
| Low-cost hardware constraints | LeRobot's efficient data format + careful batch sizing for training |

---

## Insights

This project taught me how to think in pipelines—from raw teleop data to deployable policies—and that data quality trumps quantity every time. I walked away with a solid grasp of imitation learning fundamentals, the patience to debug hardware-software interfaces, and the confidence that I can ship something end-to-end on a shoestring budget. This is groundwork I'll carry into every robotics project from here: understanding the full stack lets me make better choices at each layer. More than that, it's my first step toward combining AI and robotics for autonomy—I see this as the foundation for scaling to more complex tasks, multi-agent setups, and eventually systems that can adapt and generalize. This is where I'm building from.

## Resources

- [LeRobot](https://huggingface.co/lerobot)
- [LeRobot (GitHub)](https://github.com/huggingface/lerobot)
- [SO-ARM100 / SO-101](https://github.com/TheRobotStudio/SO-ARM100)
