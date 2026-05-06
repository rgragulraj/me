---
title: "Mars Scout Rover — IMU Navigation Subsystem"
date: "Spring 2026"
summary: Designed and built a custom IMU navigation board from scratch—schematic, PCB layout, firmware, and UART protocol—as one of seven modular subsystems on a team-built Mars rover.
---

<div class="mars-imu-carousel" data-carousel-index="0" style="position: relative; display: flex; align-items: center; gap: 0.75rem; max-width: 100%; margin: 1rem 0;">
  <button type="button" aria-label="Previous" onclick="var c=this.parentNode;var s=c.querySelectorAll('.mars-imu-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)-1+3)%3;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});" style="flex-shrink: 0; width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); background: rgba(255,255,255,0.1); color: #fff; font-size: 1.25rem; cursor: pointer; display: flex; align-items: center; justify-content: center;">‹</button>
  <div style="flex: 1; aspect-ratio: 16/9; min-height: 200px; background: rgba(255,255,255,0.06); border-radius: 6px; overflow: hidden; position: relative;">
    <div class="mars-imu-slide" style="width:100%;height:100%;position:absolute;inset:0;"><img src="./314image1.jpg" alt="Mars Scout Rover IMU Navigation Subsystem - PCB Photo 1" style="width: 100%; height: 100%; object-fit: contain; border-radius: 6px;" /></div>
    <div class="mars-imu-slide" style="width:100%;height:100%;position:absolute;inset:0;display:none;"><img src="./314image2.jpg" alt="Mars Scout Rover IMU Navigation Subsystem - PCB Photo 2" style="width: 100%; height: 100%; object-fit: contain; border-radius: 6px;" /></div>
    <div class="mars-imu-slide" style="width:100%;height:100%;position:absolute;inset:0;display:none;"><iframe src="https://www.youtube.com/embed/OUy0Lak9kGo" title="Mars Scout Rover IMU Navigation Subsystem - Demo Video" style="width:100%;height:100%;border:none;" allowfullscreen></iframe></div>
  </div>
  <button type="button" aria-label="Next" onclick="var c=this.parentNode;var s=c.querySelectorAll('.mars-imu-slide');var i=(parseInt(c.getAttribute('data-carousel-index'),10)+1)%3;c.setAttribute('data-carousel-index',i);s.forEach(function(el,j){el.style.display=j===i?'block':'none';});" style="flex-shrink: 0; width: 36px; height: 36px; border-radius: 50%; border: 1px solid rgba(255,255,255,0.4); background: rgba(255,255,255,0.1); color: #fff; font-size: 1.25rem; cursor: pointer; display: flex; align-items: center; justify-content: center;">›</button>
</div>

_EGR 314 | Arizona State University | Spring 2026 | Team 305 (7-person team)_  
_Professor: [Kevin Nichols](https://www.linkedin.com/in/kevin-nichols-45180b73/)_

## Tech Stack / Platform

KiCad · PCB Design · ESP32-S3 · Embedded C · I2C · UART · LSM9DS1 (9-DOF IMU) · Buck Regulator · Power Budgeting · SMD Soldering · Systems Integration · Embedded Firmware

## Abstract

Team 305 built a remotely operated Mars Scout Rover for a planetary exploration simulation. The rover architecture was modular: seven team members each designed a custom PCB subsystem (mobility, environmental sensing, obstacle detection, navigation, imaging, wireless communications, and HMI).

All seven boards communicated over a shared daisy-chained UART bus using a custom 16-message-type protocol, streaming real-time telemetry and video to a laptop base station.

My role was the IMU / Navigation Subsystem: the board responsible for real-time orientation, tilt, acceleration, and heading.

---

## Content

### My Subsystem Build

#### Hardware

- Designed a custom 2-layer PCB in KiCad from scratch (schematic capture, layout, DRC/ERC, and fabrication handoff)
- Used an ESP32-S3-WROOM-1 as the main MCU (WiFi-capable, 240 MHz dual-core)
- Integrated an LSM9DS1 9-axis IMU for gyroscope, accelerometer, and magnetometer sensing
- Implemented LM2575-3.3BU buck regulation to step 12V barrel input down to a stable 3.3V rail
- Added board-level protection and support circuitry: 1A overcurrent fuse, I2C pull-ups, status LEDs, and USB Micro-B debug interface
- Hand-soldered all SMD components on the board

#### Firmware / Protocol

- Wrote ESP32 firmware implementing the Team 305 UART daisy-chain bus protocol
- Used a 64-byte fixed-frame UART format at 9600 baud, 8N1
- Implemented the complete receiver state machine:
  - Framing sync (`0xA5 0x5A`)
  - Byte stuffing and unstuffing
  - Packet routing across nodes
  - ACK handling
- Assigned gyro node ID `0x52` and broadcast packed `gx/gy/gz` as little-endian `int16` (`<hhh>`)
- Implemented request-response interoperability:
  - Receives `0x14` request from HMI node
  - Responds with `0x04` gyro data packet
- Validated interoperability with all six other team nodes (mixed ESP32 + MicroPython environments)

#### Power Design

- Completed full 3.3V rail power budgeting
- Modeled worst-case and low-power operating scenarios
- Verified regulator loading and expected efficiency across active components

### Highlights

> 7-person team, 7 custom PCBs, 1 shared UART bus.
> Full hardware stack: schematic -> layout -> fab -> solder -> firmware.
> 9-DOF IMU: gyroscope + accelerometer + magnetometer.
> Custom 64-byte fixed-frame UART protocol with byte stuffing, routing, and ACK.

---

## Resources

- [View Datasheet](https://rrangasa.github.io/EGR314raj.github.io/)
- [View Team Report](https://egr314-s-2026-30.github.io/EGR314-S-2026-305.github.io/)
