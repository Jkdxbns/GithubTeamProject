# 6DOF Robot Arm - Color Box Segregation

A 6-DOF arm that spots colored boxes and sorts them into matching bins. We design it in
CAD, simulate it in Gazebo, plan motion with MoveIt 2, and drive it with a camera (RGB-D
plus color detection). Later on we move it into Isaac Sim and train a policy. It's a
simulation-only project.

## Task

Sort 42 boxes (5x5x5 cm, six colors: Red, Blue, Green, Black, White, Light Blue) out of
one base bin into six colored bins. The arm is based on the AR4, with a two-finger
gripper and a wrist-mounted RGB-D camera.

## Stack

- CAD: SolidWorks + Fusion 360, exported to URDF with sw2urdf
- Middleware: ROS 2 Jazzy
- Sim: Gazebo, then Isaac Sim
- Planning: MoveIt 2
- Perception: RGB-D plus HSV/YOLO color detection and IK

## Contents

- CAD - arm design files (native plus shared STEP)

## CAD exchange format

We use STEP (.step / .stp) to move parts between tools, since SolidWorks and Fusion 360
both read and write it. Keep the native files too (.SLDPRT, .SLDASM, .f3d).

## Working with the repo

CAD files are stored with Git LFS, so run `git lfs install` after cloning. Work on a
feature/<name> branch, open a PR, get one review, then merge to main.
