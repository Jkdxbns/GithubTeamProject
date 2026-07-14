# CAD

Design files for the arm. Every collaborator follows the structure and naming below
so the master assembly stays clean and merges stay predictable. The rules are strict.
Files that do not follow them are sent back on review.

## Folder structure

Each subassembly has one folder. Create it if it does not exist and put your files only
inside your own folder.

```
CAD/
  01_base/            Fixed base, J1 yaw housing and motor
  02_shoulder/        Link 1, J2 pitch, motor and bracket
  03_upper_arm/       Link 2, J3 pitch, motor and bracket
  04_forearm/         Link 3, J4 roll, motor and bracket
  05_wrist/           Links 4 and 5, J5 and J6, flange
  06_end_effector/    2-finger claw, fingertip switch, RGB-D mount
  master/             Master assembly and combined STEP (PM only)
```

Inside every subassembly folder use these two subfolders:

```
01_base/
  native/    SolidWorks or Fusion source files (.SLDPRT, .SLDASM, .f3d)
  step/      STEP export of the finished subassembly (.step)
```

## What goes where

| File type | Folder | Notes |
|---|---|---|
| .SLDPRT, .SLDASM | `native/` | SolidWorks parts and subassembly |
| .f3d | `native/` | Fusion 360 source |
| .step / .stp | `step/` | One STEP export of the full subassembly |
| Master assembly and combined STEP | `master/` | PM only, do not add here |

Do not commit backups, autosave copies, temp files, or exports from other tools.

## Naming convention

- Lowercase, words joined by underscores, no spaces, no capitals.
- Prefix every file with its subassembly number and name.
- Parts: `NN_subassembly_part.SLDPRT`  (example: `02_shoulder_bracket.SLDPRT`)
- Subassembly: `NN_subassembly.SLDASM`  (example: `02_shoulder.SLDASM`)
- STEP export: `NN_subassembly.step`  (example: `02_shoulder.step`)
- No version tags in filenames. Do not add `v1`, `v2`, `final`, or dates. Git keeps the
  history.

## Tools to install

Install both before pushing.

- Git: https://git-scm.com/downloads
- Git LFS: https://git-lfs.com

CAD files are stored with Git LFS. Run this once after cloning:

```
git lfs install
```

## Branches and pushing

Each owner works on their own branch, named after their folder. The PM merges every
branch and resolves any conflicts.

1. Clone and enter the repo:
   ```
   git clone git@github.com:Jkdxbns/GithubTeamProject.git
   cd GithubTeamProject
   git lfs install
   ```
2. Create your branch from main:
   ```
   git checkout main
   git pull
   git checkout -b feature/NN_name
   ```
   Example: `feature/02_shoulder`.
3. Add only files inside your own subassembly folder:
   ```
   git add CAD/02_shoulder
   git commit -m "Add shoulder parts and STEP export"
   git push -u origin feature/NN_name
   ```
4. Open a pull request into main. Do not merge it yourself.

The PM reviews each pull request, merges into main, and resolves conflicts. Keeping each
subassembly in its own folder means changes stay separated and merges stay clean.
