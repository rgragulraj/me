---
title: "Segmented Policy Execution on the SO101 Arm Using the LeRobot Framework"
date: "March 2026 - Ongoing"
summary: "Ongoing work on segmented policy execution for the SO101 robotic arm using the LeRobot framework."
---

<div style="aspect-ratio: 16/9; width: 100%; margin: 1rem 0;">
  <iframe
    src="https://www.youtube.com/embed/ZLI1b6HK4bE?autoplay=1&mute=1&playsinline=1"
    title="Segmented Policy Execution on the SO101 Arm Using the LeRobot Framework"
    style="width:100%;height:100%;border:none;border-radius:8px;"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen
  ></iframe>
</div>

## Objective

This project runs multiple policies in sequence on the SO101 arm to test whether one policy can reliably hand off to the next. The core idea is that different subtasks within a manipulation task respond better to different policy behaviors. For example, in a pick-and-insert task, locating and approaching an object calls for a generalized policy since the object can be anywhere in the workspace, while the actual grasp needs a precise policy to get it right. The same logic applies to insertion: move to the target with a generalized policy, then insert with a precise one. Each policy is a modified version of a lightweight architecture like ACT, tuned specifically for its subtask, and the goal is to show that this kind of pipeline can be both generalizable and precise where it counts.

## Procedure

### What I Have Done / What I Am Doing

This is an ongoing project, and this section will be updated as progress continues. The notes below reflect the current implementation state.

### Current State: Two-Policy Pipeline

The system currently runs two policies in sequence on the SO101 arm:

- **Policy 1 (pick and approach):** Picks up a block from anywhere in the workspace and brings it to a hover around 4 cm above the slot with roughly correct orientation. It stops before insertion.
- **Policy 2 (precision insertion):** Takes over at hover and performs insertion. It uses the wrist camera to make small visual corrections before moving the block into the slot.

### Handoff Logic

The handoff is triggered visually. Policy 2 activates when the wrist camera sees the slot centered and sufficiently large in the frame, with detection smoothed over multiple frames to reject transient errors.

A fixed Z-height trigger would be simpler, but this visual trigger ties the switch condition to what the camera actually observes rather than only to the arm's estimated position.

### Policy Configuration

Both policies are based on ACT, but each is tuned for its specific subtask:

- **Policy 1:** Chunk size `100` for long, coarse pick-and-approach motion.
- **Policy 2:** Chunk size `20` with replanning every frame to support frequent mid-motion corrections needed during insertion.

### Development Order

Policy 2 is being developed first. Its operating envelope defines what Policy 1 must provide at handoff, so the precision stage is stabilized before focusing on how broadly Policy 1 generalizes. The full two-policy pipeline is evaluated once both policies are reliable in isolation.
