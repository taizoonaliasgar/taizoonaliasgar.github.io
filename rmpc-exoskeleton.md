[← Back to Home](./)

# Robust MPC for a Tremor-Suppression Wrist Exoskeleton (TAWE)

**ASME Journal of Dynamic Systems, Measurement, and Control** (accepted, in press) · T. Chunawala, S. Janakaraj, J. Decker, M. Ahmad, S. Vijayan, O. Barry, K. Akbari Hamed  
🎥 [Video](https://www.youtube.com/watch?v=X2gqHbkB6GM) · 📄 Paper link coming soon

This project develops a **robust model predictive controller (RMPC)** for the **Tremor Alleviating Wrist Exoskeleton (TAWE)**. It suppresses essential-tremor motion while preserving voluntary wrist movement. Instead of reacting to tremor after it happens, the controller **plans in advance for the worst-case tremor disturbances**.

> All controller results are from **simulation**. The tremor data used to build and test the controller was **recorded from essential-tremor patients** wearing TAWE.

---

## 🎥 Video

▶️ **[Watch the project video](https://www.youtube.com/watch?v=X2gqHbkB6GM)** (about 2.5 minutes)

---

## 🦾 System

- **Device:** TAWE, a 6-DoF passive linkage with **2 actuated joints**: wrist flexion/extension (FE, up-down) and radial/ulnar deviation (RUD, side-to-side)
- **Model:** the 9-DoF arm–exoskeleton system, reduced through its holonomic constraints to a 2-DoF wrist model for real-time control
- **Tremor data:** recorded with TAWE in passive mode during standard clinical tasks. ET patients show distinct power peaks in the **4–12 Hz** band.

<div style="text-align:center; margin-bottom: 24px;">
  <img src="assets/exoskeleton/TAWE.png" alt="Tremor Alleviating Wrist Exoskeleton (TAWE) worn on the forearm" style="max-width: 85%; border-radius: 10px;">
  <p style="margin-top: 8px;"><em>The Tremor Alleviating Wrist Exoskeleton (TAWE).</em></p>
</div>

---

## 🧠 Approach

- **One branch per extreme disturbance:** tremor torque is mapped to joint-velocity deviations, and a **convex hull with 4 vertices** bounds them. The RMPC predicts one branch for each vertex, with its own cost and constraints.
- **One combined optimization:** branch costs are summed and constraints are stacked, and all branches **share the same first control input**, which is the action applied now.
- **State-dependent cost weighting (key contribution):** each branch is weighted by how closely its disturbance aligns with the current tracking error, so the controller **prioritizes the tremor currently pushing the wrist off course**. This avoids the sluggish, overly conservative behavior of equal weighting.
- **Real-time:** 20 ms sampling, prediction horizon N = 15, mean solve time **14.6 ms** (MATLAB, desktop).

---

## 📊 Results (simulation)

**Benchmark tremor** (amplitude-modulated sinusoids, 3–7 Hz). Tracking error, RMSE in rad (lower is better):

| Joint | MPC | NMPC | MPC-NDO | **RMPC** |
|---|---|---|---|---|
| Side-to-side (RUD) | 0.031 | 0.030 | 0.015 | **0.010** |
| Up-down (FE) | 0.072 | 0.074 | 0.035 | **0.028** |

RMPC has **20–33% lower error** than MPC-NDO, an MPC augmented with a nonlinear disturbance observer and the strongest baseline. The observer reacts with a phase lag, while RMPC corrects proactively.

**Stress tests** versus MPC-NDO:
- **Sensor noise (0.01 rad):** MPC-NDO amplifies the noise, and RMPC keeps **up to 46% lower** error.
- **50% actuation latency:** both controllers perform comparably.

**Patient-derived tremor:** RMPC cuts tracking error by **up to 47%** versus MPC-NDO (RMSE 0.015 / 0.032 vs. 0.024 / 0.060 rad).

<div style="display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;">
  <div style="text-align: center; width: 45%;">
    <div style="height: 260px; display: flex; align-items: center; justify-content: center;">
      <img src="assets/exoskeleton/steady_reference_tracking3.png" alt="Constant-reference wrist tracking under tremor disturbance" style="max-width: 100%; max-height: 100%; object-fit: contain;">
    </div>
    <p style="margin-top: 8px;"><em>Constant reference: RMPC (red) vs. nominal MPC (blue) under tremor disturbance.</em></p>
  </div>
  <div style="text-align: center; width: 45%;">
    <div style="height: 260px; display: flex; align-items: center; justify-content: center;">
      <img src="assets/exoskeleton/sin_reference_tracking3.png" alt="Sinusoidal-reference wrist tracking under tremor disturbance" style="max-width: 100%; max-height: 100%; object-fit: contain;">
    </div>
    <p style="margin-top: 8px;"><em>Sinusoidal reference: RMPC (red) vs. nominal MPC (blue) under tremor disturbance.</em></p>
  </div>
</div>

---

## 🛠️ What I built

- The reduced-order wrist model and the RMPC formulation with state-dependent cost weighting
- The data-driven convex uncertainty set derived from tremor torques
- The benchmark against MPC, NMPC and MPC-NDO, including noise, latency and patient-data stress tests

---

## 🔗 Related Project

- [Multi-Rate NMPC for Wall-Supported Bipedal Locomotion](bipedal-mr-nmpc5.md)

[← Back to Home](./)
