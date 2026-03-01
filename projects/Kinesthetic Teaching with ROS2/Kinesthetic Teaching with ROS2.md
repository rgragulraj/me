---
title: "Kinesthetic Teaching with ROS2"
date: "February 2025"
summary: Learning ROS2 by implementing kinesthetic teaching on the SO-101 arm—recording and replaying motions by physically guiding the robot and playing them back via ROS2 nodes and topics.
---

<iframe width="100%" height="400" src="https://www.youtube.com/embed/42STxw2Ngu0" title="Kinesthetic Teaching with ROS2" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen style="border-radius: 8px; margin: 1rem 0;"></iframe>

## Objective

This project is a hands-on way to **learn ROS2**: use the SO-101 arm to do kinesthetic teaching (teach by demonstration), then replay the recorded motions through a small ROS2 workflow. The goal is to get comfortable with ROS2 concepts—nodes, topics, and the publish/subscribe model—while doing something concrete on real hardware.

## Setup

- **Robot:** SO-101 arm  
- **Middleware:** ROS2  
- **Idea:** Physically move the arm through a desired motion (kinesthetic teaching), record joint positions (or similar) as the motion is executed, then publish and replay that trajectory using ROS2 nodes.

## What I did

I used the SO-101 arm to record motions by physically guiding it, then replayed those motions via ROS2. That meant writing or using nodes that publish joint states or trajectory messages and others that subscribe and drive the arm, so the same motion could be repeated. Along the way I touched topics, message types, and the basics of the ROS2 Python client library.

## Takeaways

Kinesthetic teaching is a simple and intuitive way to get a robot to “learn” a motion without coding the path by hand. Doing it on ROS2 forced me to think in terms of nodes, topics, and messages—which made the ROS2 model stick better than only reading docs. This project is a practical stepping stone toward more advanced ROS2 workflows (e.g. motion planning, perception, or multi-robot setups) while keeping the hardware and task manageable.
