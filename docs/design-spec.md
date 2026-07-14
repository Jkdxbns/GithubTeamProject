# Design Spec

Our arm design and the sorting task. I'll keep this updated as we lock things down.

## The task

We detect colored boxes, pick them out of a base bin, and drop each one into its
matching colored bin. Everything runs in simulation.

- Boxes: 42 total, 7 of each color (Red, Blue, Green, Black, White, Light Blue),
  5x5x5 cm, under 0.5 kg each.
- Colored bins: six of them, 25x25x50 cm (LxWxH), one per color.
- Base bin: 1x1x1 m.
- Bin distance: 0.5 m from the base.

Heads up on colors: black, white and light blue are low saturation, so plain HSV hue
thresholding struggles with them. Perception will probably need the value channel for
those three.

## The arm

Six DOF, all revolute (yaw, pitch, pitch, roll, pitch, roll). We're basing it on the
AR4 and keeping its stock dimensions (~600 mm reach) so we maintain the universal style
of AR4, we design everything from scratch on CAD.

Motor sizing follows the AR4: bigger steppers on J1-J3 (base, shoulder, elbow carry
the most load), smaller ones on J4-J6 (wrist).

## Gripper and sensors

Two-finger parallel claw with more than 60 mm of jaw travel so it clears a 50 mm box.
The second finger is a mimic joint in the URDF, not a real closed loop. We put a limit
switch at the fingertip, which becomes a contact sensor in sim.

Wrist-mounted RGB-D camera (eye in hand). We dropped the 1D lidar.

For grasp detection in sim we use the fingertip contact sensor plus a jump in joint
effort. We also need a Gazebo grasp-fix plugin, otherwise the gripper drops the box.

## CAD split (one subassembly each)

| Owner | Subassembly | Contains |
|---|---|---|
| A | Base + turntable | Fixed base, J1 yaw housing + motor |
| B | Shoulder | Link 1, J2 pitch, motor/bracket |
| C | Upper arm | Link 2, J3 pitch, motor/bracket |
| D | Forearm | Link 3, J4 roll, motor/bracket |
| E | Wrist | Links 4+5, J5 & J6, flange |
| F | End effector + sensors | 2-finger claw, fingertip switch, RGB-D mount + body |

I own the master assembly, the interface sheet (junction faces and the frame
convention everyone follows), and the sw2urdf export.

## Export formats

| Format | Purpose |
|---|---|
| .SLDPRT / .SLDASM / .f3d | Native editable source (per tool) |
| .STEP / .stp | Shared format between SolidWorks and Fusion, and for the master assembly |
| URDF + .STL/.dae | Simulation (Gazebo/MoveIt/Isaac), from sw2urdf |

## sw2urdf gotchas

Things that break the export if we miss them:

- Assign a material/density to every part, or the mass and inertia export as zero.
- Keep all mates, coordinate systems and axes at the assembly (.SLDASM) level, not
  inside the part files.
- At each joint, line up the Z-axis with the motion axis.
- Keep the meshes folder next to the URDF (the paths are relative).
- Expect the robot to come in rotated ~90 degrees in RViz; that's a normal RPY fix.
- sw2urdf doesn't generate any controllers, so we add the ros2_control YAML ourselves.
