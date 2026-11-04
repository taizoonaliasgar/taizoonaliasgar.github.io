[← Back to Home](./)

# Robust MPC for a Tremor-Suppression Wrist Exoskeleton (TAWE)

**ASME Journal of Dynamic Systems, Measurement, and Control** (accepted, in press) · T. Chunawala, S. Janakaraj, J. Decker, M. Ahmad, S. Vijayan, O. Barry, K. Akbari Hamed  
🎥 [Video](https://www.youtube.com/watch?v=X2gqHbkB6GM) · 📄 Paper link coming soon

This project develops a **robust model predictive controller (RMPC)** for the **Tremor Alleviating Wrist Exoskeleton (TAWE)**. It suppresses essential-tremor motion while preserving voluntary wrist movement. Instead of reacting to tremor after it happens, the controller **plans in advance for the worst-case tremor disturbances**.

> All controller results are from **simulation**. The tremor data used to build and test the controller was **recorded from essential-tremor patients** wearing TAWE.

---

## 🦾 System

- **Device:** TAWE, a 6-DoF passive linkage with **2 actuated joints**: wrist flexion/extension (FE, up-down) and radial/ulnar deviation (RUD, side-to-side)
- **Model:** The 9-DoF arm–exoskeleton system, reduced through its holonomic constraints to a 2-DoF wrist model for real-time control
- **Tremor Data:** Recorded with TAWE in passive mode during standard clinical tasks. ET patients show distinct power peaks in the **4–12 Hz** band.

<div style="text-align:center; margin-bottom: 24px;">
  <img src="assets/exoskeleton/TAWE.png" alt="Tremor Alleviating Wrist Exoskeleton (TAWE) worn on the forearm" style="max-width: 85%; border-radius: 10px;">
  <p style="margin-top: 8px;"><em>The Tremor Alleviating Wrist Exoskeleton (TAWE).</em></p>
</div>

---

## 🧠 Approach

- **One Branch per Extreme Disturbance:** Tremor torque is mapped to joint-velocity deviations, and a **convex hull with 4 vertices** bounds them. The RMPC predicts one branch for each vertex, with its own cost and constraints.
- **One Combined Optimization:** Branch costs are summed and constraints are stacked, and all branches **share the same first control input**, which is the action applied now.
- **State-Dependent Cost Weighting (Key Contribution):** Each branch is weighted by how closely its disturbance aligns with the current tracking error, so the controller **prioritizes the tremor currently pushing the wrist off course**. This avoids the sluggish, overly conservative behavior of equal weighting.
- **Real-Time:** 20 ms sampling, prediction horizon N = 15, mean solve time **14.6 ms** (MATLAB, desktop).

---

## 📊 Results (Simulation)

**Benchmark Tremor** (amplitude-modulated sinusoids, 3–7 Hz, applied between 3 and 7 s). Solid lines show side-to-side (RUD) motion and dashed lines up-down (FE) motion.

<div style="display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;">
  <div style="text-align: center; flex: 1 1 320px; max-width: 48%;">
    <img src="assets/exoskeleton/tracking_constant_reference.png" alt="Wrist tracking of a constant reference under tremor: RMPC (orange) stays closest to the reference, compared with MPC, NMPC and MPC-NDO" style="width: 100%;">
    <p style="margin-top: 8px;"><em>Constant reference</em></p>
  </div>
  <div style="text-align: center; flex: 1 1 320px; max-width: 48%;">
    <img src="assets/exoskeleton/tracking_timevarying_reference.png" alt="Wrist tracking of a time-varying reference under tremor: RMPC (orange) follows the reference most closely, compared with MPC, NMPC and MPC-NDO" style="width: 100%;">
    <p style="margin-top: 8px;"><em>Time-varying reference</em></p>
  </div>
</div>

Tracking error, RMSE in rad (lower is better):

| Joint | MPC | NMPC | MPC-NDO | **RMPC** |
|---|---|---|---|---|
| Side-to-side (RUD) | 0.031 | 0.030 | 0.015 | **0.010** |
| Up-down (FE) | 0.072 | 0.074 | 0.035 | **0.028** |

RMPC has **20–33% lower error** than MPC-NDO, an MPC augmented with a nonlinear disturbance observer and the strongest baseline. The observer reacts with a phase lag, while RMPC corrects proactively.

**Stress Tests** versus MPC-NDO:
- **Sensor Noise (0.01 rad):** MPC-NDO amplifies the noise, and RMPC keeps **up to 46% lower** error.
- **50% Actuation Latency:** Both controllers perform comparably.

**Patient-Derived Tremor:** RMPC cuts tracking error by **up to 47%** versus MPC-NDO (RMSE 0.015 / 0.032 vs. 0.024 / 0.060 rad).


---

## 🛠️ What I Built

- The reduced-order wrist model and the RMPC formulation with state-dependent cost weighting
- The data-driven convex uncertainty set derived from tremor torques
- The benchmark against MPC, NMPC and MPC-NDO, including noise, latency and patient-data stress tests

---

## 🔗 Related Project

- [Multi-Rate NMPC for Wall-Supported Bipedal Locomotion](bipedal-mr-nmpc5.md)

[← Back to Home](./)
