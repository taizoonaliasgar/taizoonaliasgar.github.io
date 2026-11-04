[← Back to Home](./)

# Multi-Rate NMPC for Wall-Supported Bipedal Locomotion of Quadrupedal Robots

**IEEE/RSJ IROS 2026** · T. Chunawala, J. Kim, K. Akbari Hamed  
📄 [Paper (arXiv)](https://arxiv.org/abs/2607.01574) · 🎥 [Video](https://www.youtube.com/watch?v=N6XwNJ0E9s0)

This project lets a quadrupedal robot walk upright on its rear legs while bracing its front legs against nearby walls, for tight corridors and cluttered spaces. A **multi-rate nonlinear MPC (MR-NMPC)** plans the slow-updating footstep locations and the fast-updating body trajectory **together in one optimization**, instead of relying on a heuristic foot-placement rule.

---

## 🎥 Video

▶️ **[Watch the project video](https://www.youtube.com/watch?v=N6XwNJ0E9s0)**: simulation results and preliminary hardware experiments.

---

## 🎯 Problem

- An upright, wall-supported posture is **underactuated, hybrid and dynamically unstable**, with brief, small-area contacts.
- Body motion, contact forces and foot placement are **strongly coupled**, and they evolve at different rates.
- Standard MPC assumes uniform input rates and usually places feet with a **heuristic** (such as the Raibert rule), which breaks down on irregular terrain at higher speeds.

---

## 🧠 Approach

- **Multi-rate NMPC (high level):** jointly plans discrete-time footstep locations (updated once per contact phase) and continuous-time center-of-mass and orientation trajectories, using a single-rigid-body model with contact constraints.
- **Foothold propagation:** future footholds are part of the prediction dynamics, so the controller can choose **asymmetric front and rear step lengths** to keep balance.
- **Whole-body controller (low level):** a nonlinear QP controller based on virtual constraints tracks the MPC references using the full-order robot dynamics.

| Parameter | Value |
|---|---|
| High-Level MR-NMPC Rate | **100 Hz** |
| Prediction Horizon | 20 steps (200 ms) |
| Mean Solve Time | **8.26 ms** |
| Solver | CasADi / IPOPT |
| Low-Level Whole-Body Controller Rate | **1 kHz** |
| Simulation Platform | Unitree A1 in RaiSim |
| Hardware Platform | Unitree Go2 (preliminary) |

---

## 📊 Results

**Simulation (Unitree A1)**
- **2.9× higher success rate** than MPC with Raibert-heuristic foot placement: **68.8% vs. 23.6%** across **250 randomized 7 m tracks** with random wooden-block terrain, with speeds ramped up to 0.8 m/s.
- Rejects a **50 N** sinusoidal push while staying within safety and kinematic limits, by choosing shorter, asymmetric steps where the heuristic over-steps.

**Preliminary hardware (Unitree Go2)**
- Real-time deployment: the robot moves from a crouch to **upright wall-supported bipedal locomotion** and keeps its balance for **over 60 s**.
- The main limitation is noise in velocity estimation. Improving state estimation is ongoing work.

<div style="display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;">
  <div style="text-align: center; width: 45%;">
    <div style="height: 260px; display: flex; align-items: center; justify-content: center; background: #f4f4f4; border-radius: 10px; overflow: hidden;">
      <img src="assets/bipedal/thumbnail1.PNG" alt="Unitree A1 in simulation on uneven wooden-block terrain" style="max-width: 100%; max-height: 100%; object-fit: contain;">
    </div>
    <p style="margin-top: 8px;"><em>Simulation: Unitree A1 on randomized wooden-block terrain.</em></p>
  </div>
  <div style="text-align: center; width: 45%;">
    <div style="height: 260px; display: flex; align-items: center; justify-content: center; background: #f4f4f4; border-radius: 10px; overflow: hidden;">
      <img src="assets/bipedal/thumbnail2.PNG" alt="Unitree Go2 in a wall-supported upright bipedal stance" style="max-width: 100%; max-height: 100%; object-fit: contain;">
    </div>
    <p style="margin-top: 8px;"><em>Hardware: Unitree Go2 in wall-supported bipedal locomotion.</em></p>
  </div>
</div>

---

## 🛠️ What I built

- The MR-NMPC formulation and its CasADi/IPOPT implementation
- A multithreaded real-time C++ control stack linking the NMPC to the whole-body controller
- A 1 kHz kinematics–IMU state estimator for hardware deployment
- The randomized-terrain benchmark against the Raibert heuristic

---

## 🔗 Related Project

- [Robust MPC for a Tremor-Suppression Exoskeleton](rmpc-exoskeleton.md)

[← Back to Home](./)
