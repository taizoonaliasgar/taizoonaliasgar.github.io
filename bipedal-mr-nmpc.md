# Multi-Rate NMPC for Wall-Supported Bipedal Locomotion

This project develops a multi-rate nonlinear MPC (MR-NMPC) framework for wall-supported bipedal locomotion on the Unitree Go2, achieving a 13× improvement in uneven terrain traversal.

## Overview
- Robot: Unitree Go2
- Task: Wall-supported bipedal locomotion over uneven terrain
- Key idea: Multi-rate NMPC with separate update rates for step length and whole-body control

## Experimental Results

<!-- Example image: replace with your actual file/path -->
![Unitree Go2 wall-supported bipedal locomotion](assets/bipedal/exp1.png)

You can briefly describe each image here: terrain type, controller settings, success metrics, etc.

## Technical Highlights
- Multi-rate NMPC structure (3 Hz for footstep updates, 50 Hz for whole-body control)
- Robustness to terrain uncertainty
- Integration with whole-body controller

## Related Work / Links
- [Back to Home](./)  
