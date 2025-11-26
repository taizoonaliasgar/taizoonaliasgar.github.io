[← Back to Home](./)

# Multi-Rate NMPC for Wall-Supported Bipedal Locomotion (Unitree Go2)

This project demonstrates a **real-time Multi-Rate Nonlinear Model Predictive Controller (MR-NMPC)** that enables a **Unitree Go2 quadruped to rise into an upright, wall-supported bipedal posture and locomote over uneven terrain** with high reliability.

The system runs **fully on hardware** and integrates **footstep planning, force optimization, and whole-body control in a single loop**.

---

## 🔧 System Overview

- **Robot:** Unitree Go2  
- **Control Stack:**  
  - High-level planner: **Multi-Rate NMPC**  
  - Low-level tracking: **Hybrid Zero Dynamics Whole-Body Controller (500 Hz)**  
- **Update Rates:**  
  - Footstep planning: **3 Hz (slow loop)**  
  - Reaction-force & CoM control: **50 Hz (fast loop)**  
- **Deployment:** Real-time on physical robot

---

## 🎯 Problem Addressed

Traditional MPC-based walking controllers struggle on:
- **Sparse and changing footholds**
- **Highly unstable upright configurations**
- **Rapid contact transitions**

This project solves these challenges by **optimizing footsteps, reaction forces, and body motion jointly** instead of treating step planning as a heuristic pre-process.

---

## 🚀 Key Innovations

- **Multi-rate optimization:** Footsteps and forces updated at different real-time rates  
- **Unified optimization:** CoM motion, forces, and discrete footsteps solved together  
- **Contact-aware planning:** Upcoming contact domain embedded inside MPC prediction  
- **Hardware-validated:** Fully deployed on physical robot (no offline-only results)

---

## 🧪 Experimental Setup

- **Environment:** Random wooden-block terrain with limited footholds  
- **Configuration:** Dynamically unstable upright bipedal posture  
- **Stabilization strategy:** Monkey-like contact sequence using front limbs for torso stabilization during transitions  

```md
![Hardware experimental setup](assets/bipedal/go2_setup.png)
![Wall-supported bipedal locomotion sequence](assets/bipedal/go2_sequence.png)
