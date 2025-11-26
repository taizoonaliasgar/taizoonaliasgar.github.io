[← Back to Home](./)

# Multi-Rate NMPC for Wall-Supported Bipedal Locomotion (Unitree Go2)

This project demonstrates a **real-time Multi-Rate Nonlinear Model Predictive Controller (MR-NMPC)** that enables a **Unitree Go2 quadruped to rise into an upright, wall-supported bipedal configuration and locomote over uneven terrain** with high reliability.

The system is **fully deployed on hardware** and integrates:
- Footstep planning  
- Reaction force optimization  
- Whole-body tracking  

in a **single real-time control pipeline**.

---

## 🎥 Hardware Demonstration & Technical Overview (Primary Reference)

▶️ **[Watch the full project video](https://youtu.be/_dyIMfccwPk)**

This video includes:
- The complete **multi-rate control architecture**
- Key **performance plots & baseline comparisons**
- **Hardware experiments** on the physical Unitree Go2

> 📌 *For technical details, controller structure, and quantitative results, please refer to the video above — it serves as the primary technical reference for this project.*

---

## 🔧 System Overview

- **Robot:** Unitree Go2  
- **Hierarchical Control Stack:**
  - High-level planner: **Multi-Rate NMPC(50 Hz)**
  - Low-level tracking: **Whole-Body Controller(500 Hz)**
- **Update Rates:**
  - Footstep planning: **3 Hz**
  - Reaction forces & CoM control: **50 Hz**

---

## 🎯 Problem Addressed

Agile upright locomotion demands fast, reliable footstep planning under rapidly changing contact and support conditions. Errors in contact timing or foothold selection directly lead to loss of balance and failure.

- Upright configurations are **dynamically unstable**
- Motion, contact forces, and foot placement are **strongly coupled**
- Traditional MPC uses **heuristic footstep planning**, limiting robustness

This work overcomes these limitations by **jointly optimizing footsteps, forces, and body motion inside a single real-time MPC**, enabling robust locomotion under severe terrain and contact uncertainty.


---

## 🚀 Key Contributions

- **Unified optimization** of CoM motion, reaction forces, and discrete footsteps
- **Multi-rate real-time execution** enabling both fast stabilization and slow step adaptation
- **Contact-aware prediction**, allowing anticipation of upcoming contact domains
- **Fully hardware validated** on a dynamically unstable upright robotic configuration

---

## 🧪 Experimental Setup

- **Environment:** Random wooden-block terrain with limited and uneven footholds  
- **Configuration:** Dynamically unstable upright bipedal posture  
- **Stabilization strategy:** Monkey-like contact sequencing using front limbs for torso stabilization during transitions

📷 **Representative simulation & hardware photos**
<div style="display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;">

  <!-- Left image (landscape) -->
  <div style="text-align: center; width: 45%;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #f4f4f4;
      border-radius: 10px;
      overflow: hidden;">
      
      <img src="assets/bipedal/thumbnail1.PNG"
           style="max-width: 100%; max-height: 100%; object-fit: contain;">
    </div>
    <p style="margin-top: 8px;">
      <em>Unitree A1 traversing an uneven wooden-block terrain under uncertainty.</em>
    </p>
  </div>

  <!-- Right image (portrait) -->
  <div style="text-align: center; width: 45%;">
    <div style="
      height: 260px;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #f4f4f4;
      border-radius: 10px;
      overflow: hidden;">
      
      <img src="assets/bipedal/thumbnail2.PNG"
           style="max-width: 100%; max-height: 100%; object-fit: contain;">
    </div>
    <p style="margin-top: 8px;">
      <em>Wall-supported upright bipedal locomotion of Unitree Go2 under MR-NMPC control.</em>
    </p>
  </div>

</div>


---

## 📊 Key Results (From Hardware & Simulation)

- **13× improvement** in uneven terrain traversal distance: **MR-NMPC:** ~66% vs **Raibert heuristic baseline:** <5%
- Successful **crouch → stand → sustained bipedal trot in place**
- Robust recovery from:
  - Terrain height uncertainty
  - External contact disturbances
  - Contact switching events

All plots and performance breakdowns are shown in the **project video above**.

---

## 📄 Technical Documentation (Optional Deep Dive)

For full mathematical formulation and control architecture:

📄 **[Download Conference Poster (PDF)](assets/bipedal/bipedal_MRNMPC.pdf)**

(This contains the full MR-NMPC formulation, architecture diagram, and quantitative plots.)

---

## 🏭 Industry Relevance

This work directly applies to:

- **Industrial inspection robots**
- **Search & rescue platforms**
- **Legged manipulation in cluttered environments**
- **Real-time contact-rich motion planning**

Core engineering skills demonstrated:
- Real-time optimal control
- Multi-rate control design
- Contact modeling
- Whole-body control
- Hardware deployment & testing

---

## 🔗 Related Project

- [Robust MPC for Tremor-Suppression Exoskeleton](rmpc-exoskeleton.md)

[← Back to Home](./)
