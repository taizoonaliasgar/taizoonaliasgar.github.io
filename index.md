---
title: "About"
feature_row_lead:
  - image_path: /assets/bipedal/thumbnail2.PNG
    alt: "Unitree Go2 standing upright between two walls, bracing its front legs against them"
    title: "Multi-Rate NMPC for Wall-Supported Bipedal Locomotion"
    excerpt: "**IEEE/RSJ IROS 2026.** A multi-rate NMPC that jointly plans footsteps and body motion, achieving **2.9× higher success** than a Raibert-heuristic baseline over 250 randomized rough-terrain trials (simulation), with preliminary hardware deployment on a Unitree Go2. [Paper (arXiv)](https://arxiv.org/abs/2607.01574) · [Video](https://www.youtube.com/watch?v=N6XwNJ0E9s0)"
    url: "/bipedal-mr-nmpc5.html"
    btn_label: "Project page"
    btn_class: "btn--primary"
  - image_path: /assets/exoskeleton/TAWE.png
    alt: "Tremor Alleviating Wrist Exoskeleton (TAWE)"
    title: "Robust MPC for a Tremor-Suppression Exoskeleton"
    excerpt: "**ASME JDSMC (accepted).** A robust MPC with state-dependent cost weighting that cuts tracking error by **up to 47%** versus observer-based MPC on patient-derived tremor (simulation). [Video](https://www.youtube.com/watch?v=X2gqHbkB6GM)"
    url: "/rmpc-exoskeleton.html"
    btn_label: "Project page"
    btn_class: "btn--primary"
feature_row_coauthor:
  - image_path: https://img.youtube.com/vi/SaZMqanFWv0/hqdefault.jpg
    alt: "Video thumbnail: Unitree Go2 with a Kinova arm"
    title: "Decomposition-Based NMPC for Quadrupedal Loco-Manipulation"
    excerpt: "**IEEE RA-L 2026.** Implemented the real-time interface between a 60 Hz decomposition NMPC planner and a 500 Hz QP-based whole-body controller; supported hardware validation on a Unitree Go2 carrying a 4.4 kg Kinova arm."
    url: "https://www.youtube.com/watch?v=SaZMqanFWv0"
    btn_label: "Watch video"
    btn_class: "btn--inverse"
  - image_path: https://img.youtube.com/vi/N0z3zvkmvW4/hqdefault.jpg
    alt: "Video thumbnail: team of Unitree A1 robots"
    title: "Safety-Critical Distributed NMPC for Multi-Robot Quadrupedal Teams"
    excerpt: "**IEEE RA-L 2025.** Co-developed a 100 Hz distributed nonlinear MPC for Unitree A1 robot teams; fixed real-time data-pipeline and communication-delay issues to enable stable hardware experiments."
    url: "https://www.youtube.com/watch?v=N0z3zvkmvW4"
    btn_label: "Watch video"
    btn_class: "btn--inverse"
---

I'm a **Ph.D. candidate in Mechanical Engineering at Virginia Tech** (graduating **May 2027**), working on model predictive control, trajectory optimization and whole-body control for legged robots and wearable exoskeletons.

**I'm seeking full-time roles in robot motion planning and control.**

## Projects

### Lead author

{% include feature_row id="feature_row_lead" type="left" %}

### Co-author

{% include feature_row id="feature_row_coauthor" type="left" %}

## Publications

1. **T. Chunawala**, J. Kim, K. Akbari Hamed, "Multi-Rate Nonlinear Model Predictive Control for Wall-Supported Bipedal Locomotion of Quadrupedal Robots," *IEEE/RSJ IROS*, 2026. [[arXiv]](https://arxiv.org/abs/2607.01574)
2. **T. Chunawala** et al., "Robust Model Predictive Control of a Tremor-Suppression Exoskeleton under Tremor-Induced Disturbances," *ASME Journal of Dynamic Systems, Measurement, and Control*, accepted, in press.
3. R. Sambhus, K. K. Mehta, A. M. Sadeghi, B. M. Imran, J. Kim, **T. Chunawala** et al., "A Nonlinear MPC Framework for Loco-Manipulation of Quadrupedal Robots With Non-Negligible Manipulator Dynamics," *IEEE Robotics and Automation Letters*, 2026.
4. B. M. Imran, J. Kim, **T. Chunawala** et al., "Safety-Critical and Distributed Nonlinear Predictive Controllers for Teams of Quadrupedal Robots," *IEEE Robotics and Automation Letters*, 2025.
5. L. Amanzadeh, **T. Chunawala** et al., "Predictive Control with Indirect Adaptive Laws for Payload Transportation by Quadrupedal Robots," *IEEE Robotics and Automation Letters*, 2024.
6. **T. Chunawala**, M. Ghandchi-Tehrani, J. Yan, "An Optimum Design of a Double Pendulum in Autoparametric Resonance for Energy Harvesting Applications," *Vibroengineering Procedia*, 2016.


## Skills

**Control & Planning:** Nonlinear, Robust and Distributed MPC · Trajectory Optimization · Contact Planning · Whole-Body Control (QP)  
**Software:** C++ (real-time, multithreaded) · Python · MATLAB · ROS/ROS2 · CasADi · IPOPT · OSQP · Pinocchio  
**Hardware:** Unitree Go2 · Unitree A1 · Kinova Arm
