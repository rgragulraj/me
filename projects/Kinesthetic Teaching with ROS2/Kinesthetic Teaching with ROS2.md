---
title: "Kinesthetic Teaching with ROS2"
date: "February 2025"
summary: Built a ROS2 Jazzy controller node for the SO-101 arm and a kinesthetic teaching pipeline—physically guide the arm, record the trajectory, and replay it—to learn ROS2 fundamentals on real hardware.
---

<iframe width="100%" height="400" src="https://www.youtube.com/embed/42STxw2Ngu0?autoplay=1&mute=1" title="Kinesthetic Teaching with ROS2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="border-radius: 8px; margin: 1rem 0;"></iframe>

## Tech Stack · [GitHub](https://github.com/rgragulraj/ros2_ws)

Python · ROS2 Jazzy · Ubuntu 24.04 · SO-101 6-DOF Arm · scservo_sdk · colcon

## Objective

Learn ROS2 by building something real: a controller node for the SO-101 arm and a teach-by-demonstration workflow where I physically guide the arm through a motion, record the trajectory, and play it back.

---

## What I Built

### Part 1 — ROS2 Controller Node

A ROS2 node (`so101_controller`) that owns the serial connection to the arm's six Feetech STS3215 servos via a Waveshare Bus Servo Adapter on `/dev/ttyACM0`. It publishes live joint states on `/joint_states` at 10 Hz and subscribes to `/arm/joint_goal` for movement commands. This was my entry point into ROS2—setting up the workspace with `colcon`, writing an `ament_python` package (`my_arm_pkg`), defining entry points in `setup.py`, and working with `sensor_msgs/msg/JointState` messages.

### Part 2 — Kinesthetic Teaching Pipeline

A four-script workflow for teach-by-demonstration, using direct serial control via `scservo_sdk`:

| Script | What it does |
|---|---|
| `capture_home.py` | Reads all six servo positions and saves the current pose as the home position (`config/home.json`) |
| `go_home.py` | Smoothly interpolates from the current position to home over 2 seconds at 50 Hz |
| `teach.py` | Disables torque so the arm goes limp, records joint positions at 10 Hz while I physically guide it, then re-enables torque and saves the trajectory (`data/trajectory.json`) |
| `run_demo.py` | Loads the recorded trajectory and replays it at the original timing, then returns to home |

The arm has six joints—shoulder pan, shoulder lift, elbow flex, wrist flex, wrist roll, and gripper—each driven by a Feetech STS3215 servo. Positions are converted between raw servo counts and radians (`0 rad = raw 2048`, ~651 counts per radian).

---

## Takeaways

This project forced me to think in ROS2 terms—nodes, topics, publishers, subscribers, message types—while solving a concrete problem on real hardware. The controller node gave me a solid grasp of the ROS2 workspace structure, build system (`colcon`, `ament_python`), and pub/sub model. The kinesthetic teaching pipeline taught me how to work directly with servo hardware, handle torque control, and think about trajectory recording and playback at the signal level. It's a practical foundation for more advanced ROS2 work like `ros2_control`, MoveIt, or multi-robot setups.

## Resources

- [GitHub Repository](https://github.com/rgragulraj/ros2_ws)
