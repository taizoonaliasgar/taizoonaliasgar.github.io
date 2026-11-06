---
title: "Robust MPC for a Tremor-Suppression Wrist Exoskeleton (TAWE)"
description: "Robust MPC with state-dependent cost weighting for a tremor-suppression wrist exoskeleton, cutting tracking error by up to 47% versus observer-based MPC on patient-derived tremor in simulation (ASME JDSMC, accepted)."
header:
  og_image: /assets/exoskeleton/TAWE.png
---

**ASME Journal of Dynamic Systems, Measurement, and Control** (accepted, in press) · T. Chunawala, S. Janakaraj, J. Decker, M. Ahmad, S. Vijayan, O. Barry, K. Akbari Hamed  
🎥 [Video](https://www.youtube.com/watch?v=X2gqHbkB6GM) · 📄 Paper link coming soon

This project develops a **robust model predictive controller (RMPC)** for the **Tremor Alleviating Wrist Exoskeleton (TAWE)**. It suppresses essential-tremor motion while preserving voluntary wrist movement. Instead of reacting to tremor after it happens, the controller **plans in advance for the worst-case tremor disturbances**.

> All controller results are from **simulation**. The tremor data used to build and test the controller was **recorded from essential-tremor patients** wearing TAWE.

---

## System

- **Device:** TAWE, a 6-DoF passive linkage with **2 actuated joints**: wrist flexion/extension (FE, up-down) and radial/ulnar deviation (RUD, side-to-side)
- **Model:** The 9-DoF arm–exoskeleton system, reduced through its holonomic constraints to a 2-DoF wrist model for real-time control
- **Tremor Data:** Recorded in an IRB-approved study with **3 essential-tremor participants and 3 healthy controls**. TAWE logged wrist motion in passive mode alongside **EEG and EMG** during standard clinical tasks (arm extension, nose touching, Archimedes spiral). ET participants show distinct power peaks in the **4–12 Hz** band.

<div style="text-align:center; margin-bottom: 24px;">
  <img src="/assets/exoskeleton/TAWE.png" alt="Tremor Alleviating Wrist Exoskeleton (TAWE) worn on the forearm" style="max-width: 85%; border-radius: 10px;">
  <p style="margin-top: 8px;"><em>The Tremor Alleviating Wrist Exoskeleton (TAWE).</em></p>
</div>

---

## Approach

- **One Branch per Extreme Disturbance:** Tremor torque is mapped to joint-velocity deviations, and a **convex hull with 4 vertices** bounds them. The RMPC predicts one branch for each vertex, with its own cost and constraints.
- **One Combined Optimization:** Branch costs are summed and constraints are stacked, and all branches **share the same first control input**, which is the action applied now.
- **Real-Time:** 20 ms sampling, prediction horizon N = 15, mean solve time **14.6 ms** (MATLAB, desktop).
- **Four Vertices:** Compared with 5 or 6 vertices, 4 gave the lowest side-to-side error (**0.010 vs. 0.033 rad**) with similar up-down error, and solved faster (more vertices took 16–17 ms).

---

## Key Contribution: State-Dependent Cost Weighting

Standard robust MPC weights every disturbance branch equally, so it guards against all four extremes at once and reacts sluggishly. This controller instead weights each branch by how closely its disturbance aligns with the **current tracking error**, so it **prioritizes the tremor currently pushing the wrist off course**.

For each branch ℓ, an alignment score ρ<sub>ℓ</sub> compares the tracking error δx<sub>t</sub> with the disturbance direction d<sup>ℓ</sup>. The scores are normalized into weights w<sub>ℓ</sub> = ρ<sub>ℓ</sub> / (ρ<sub>1</sub> + … + ρ<sub>4</sub>), and the controller minimizes the weighted cost **J<sub>tot</sub> = w<sub>1</sub>J<sup>1</sup> + w<sub>2</sub>J<sup>2</sup> + w<sub>3</sub>J<sup>3</sup> + w<sub>4</sub>J<sup>4</sup>**.

<div style="text-align:center; margin: 12px 0 20px 0;">
  <img src="/assets/exoskeleton/cost_weighting.png" alt="Vector diagram: four grey disturbance directions d1 to d4, the orange current tracking error, and alignment scores rho 1 to rho 4; rho 1 is largest because the error points almost along d1" style="max-width: 55%;">
  <p style="margin-top: 8px;"><em>Grey arrows: the four extreme disturbances d<sup>1</sup>–d<sup>4</sup>. Orange: the current tracking error δx<sub>t</sub>. Each ρ<sub>ℓ</sub> measures how well the error aligns with d<sup>ℓ</sup>. Here the error points almost along d<sup>1</sup>, so that branch gets the largest weight, while d<sup>2</sup>, pointing the opposite way, gets the smallest.</em></p>
</div>

---

## Results (Simulation)

**Benchmark Tremor** (amplitude-modulated sinusoids, 3–7 Hz, applied between 3 and 7 s). Solid lines show side-to-side (RUD) motion and dashed lines up-down (FE) motion.

<div style="display: flex; justify-content: center; gap: 24px; flex-wrap: wrap;">
  <div style="text-align: center; flex: 1 1 320px; max-width: 48%;">
    <img src="/assets/exoskeleton/tracking_constant_reference.png" alt="Wrist tracking of a constant reference under tremor: RMPC (orange) stays closest to the reference, compared with MPC, NMPC and MPC-NDO" style="width: 100%;">
    <p style="margin-top: 8px;"><em>Constant reference</em></p>
  </div>
  <div style="text-align: center; flex: 1 1 320px; max-width: 48%;">
    <img src="/assets/exoskeleton/tracking_timevarying_reference.png" alt="Wrist tracking of a time-varying reference under tremor: RMPC (orange) follows the reference most closely, compared with MPC, NMPC and MPC-NDO" style="width: 100%;">
    <p style="margin-top: 8px;"><em>Time-varying reference</em></p>
  </div>
</div>

<div style="display: flex; flex-direction: column; align-items: center; margin-bottom: 1em;">

<p style="text-align: center; margin-bottom: 0.5em;"><em>Tracking error, RMSE in rad (lower is better)</em></p>

<table style="display: table; width: auto; margin-left: auto; margin-right: auto;">
  <thead>
    <tr><th>Joint</th><th>MPC</th><th>NMPC</th><th>MPC-NDO</th><th><strong>RMPC</strong></th></tr>
  </thead>
  <tbody>
    <tr><td>Side-to-side (RUD)</td><td>0.031</td><td>0.030</td><td>0.015</td><td><strong>0.010</strong></td></tr>
    <tr><td>Up-down (FE)</td><td>0.072</td><td>0.074</td><td>0.035</td><td><strong>0.028</strong></td></tr>
  </tbody>
</table>

</div>

RMPC has **20–33% lower error** than MPC-NDO, an MPC augmented with a nonlinear disturbance observer and the strongest baseline.

**Why It Wins:** MPC-NDO's observer underestimates peak tremor torque and lags behind it. RMPC instead applies faster, more aggressive torque corrections ("active stiffness"), trading a smoother control input for tighter tracking.

**Stress Tests** versus MPC-NDO:
- **Sensor Noise (0.01 rad):** MPC-NDO amplifies noise; RMPC has **up to 46% lower** error.
- **50% Actuation Latency:** Both controllers perform comparably.

**Patient-Derived Tremor:** RMPC cuts tracking error by **up to 47%** versus MPC-NDO (RMSE 0.015 / 0.032 vs. 0.024 / 0.060 rad).

**Next Step:** Integrate the RMPC on the TAWE prototype for clinical trials, and tailor the uncertainty set to each patient's tremor profile, with learning-based adaptation as a future extension.


---

## What I Built

- The reduced-order wrist model and the RMPC formulation with state-dependent cost weighting
- The data-driven convex uncertainty set derived from tremor torques
- The benchmark against MPC, NMPC and MPC-NDO, including noise, latency and patient-data stress tests

---

## Related Project

- [Multi-Rate NMPC for Wall-Supported Bipedal Locomotion](/bipedal-mr-nmpc5.html)
