# 6DOF Robot Arm — Color Box Segregation

A 6-DOF robotic arm that detects colored boxes and sorts them into matching bins.
Designed in CAD, simulated in Gazebo, motion-planned with MoveIt 2, and driven by
vision (RGB-D + color detection). Final stage ports the arm to Isaac Sim with a
learned (imitation/VLA) policy. **Simulation-only** project.

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
- **Learning (final):** LeRobot / imitation / VLA

## Phases

1. CAD → URDF
2. Gazebo simulation + kinematics check
3. MoveIt 2 reachability
4. Perception (color detection + RGB-D pose) + IK
5. Full pick-place-segregate loop in Gazebo
6. Port to Isaac Sim + camera-only learned policy

## Repo layout

```
/cad      Native CAD (.SLDPRT/.SLDASM/.f3d) + shared STEP files
/urdf     sw2urdf output: URDF + meshes
/ros2_ws  ROS 2 workspace (packages)
/docs     Design specs, interface sheet, meeting notes
```

## CAD exchange format

Team uses **STEP (`.step`/`.stp`)** as the shared interchange format — both
SolidWorks and Fusion 360 read/write it. Keep native files too (`.SLDPRT`,
`.SLDASM`, `.f3d`). See [`/docs`](docs/) for the interface sheet and conventions.

## Team

6 members. Everyone rotates through all roles each phase. CAD split: one
subassembly per person (base+J1, shoulder, upper arm, forearm, wrist, gripper+camera).

## Working with the repo

CAD binaries are stored via **Git LFS** — run `git lfs install` after cloning.
Work on `feature/<name>` branches → open a PR → one review → merge to `main`.
