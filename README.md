# Ragul Raj

**Gmail:** [rgragulraj@gmail.com](mailto:rgragulraj@gmail.com) · **LinkedIn:** [linkedin.com/in/rgragulraj](https://www.linkedin.com/in/rgragulraj/)

---

This repository contains the source for my personal portfolio website.

## Site Structure

Each top-level page has a dedicated HTML entry point:

- **Overview** (`index.html`) — Intro, what I do (robotics, embedded systems, software), current role at ASU Innovation Hub, and contact links.
- **Projects** (`projectshome.html`) — List of projects with links to full write-ups. Each project has its own page with markdown content and images.
- **Experience** (`experience.html`) — Lab Technician at ASU Innovation Hub (3/2024 – Present), Internship at Unijet Pneumatics (4/2022 – 5/2022).
- **Education** (`education.html`) — B.S.E. Robotics at Arizona State University (May 2027), SSVM World School (May 2023).

## Projects Content

Project pages are stored in `projects/<slug>/<slug>.md` and rendered by `projects/project.html`.

- Example: `projects/lerobot/lerobot.md`
- Project slugs are listed in `projects/index.json`
- Additional project authoring instructions are documented in `projects/README.md`

## Featured Project

`projects/lerobot/lerobot.md` documents an imitation learning pipeline on the SO-101 arm using Hugging Face LeRobot with ACT (Action Chunking with Transformers), including closed-loop deployment and precision-focused future work.
