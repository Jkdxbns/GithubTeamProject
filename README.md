# 6DOF Robot Arm — Color Box Segregation

A 6-DOF robotic arm that detects colored boxes and sorts them into matching bins.
Designed in CAD, simulated in Gazebo, motion-planned with MoveIt 2, and driven by
vision (RGB-D + color detection). **Simulation-only** project.

## Task

Sort 42 boxes (5×5×5 cm, 6 colors — Red, Blue, Green, Black, White, Light Blue)
from one base bin into six colored bins. AR4-based arm, 2-finger gripper,
wrist-mounted RGB-D camera.

## Stack

- **CAD:** SolidWorks + Fusion 360 → URDF (via `sw2urdf`)
- **Middleware:** ROS 2 Jazzy
- **Sim:** Gazebo → Isaac Sim
- **Planning:** MoveIt 2
- **Perception:** RGB-D + HSV/YOLO color detection + IK

## Contents

- **CAD** — arm design files (native + shared STEP)

## CAD exchange format

Team uses **STEP (`.step`/`.stp`)** as the shared interchange format — both
SolidWorks and Fusion 360 read/write it. Keep native files too (`.SLDPRT`,
`.SLDASM`, `.f3d`).

## Working with the repo

CAD binaries are stored via **Git LFS** — run `git lfs install` after cloning.
Work on `feature/<name>` branches → open a PR → one review → merge to `main`.
