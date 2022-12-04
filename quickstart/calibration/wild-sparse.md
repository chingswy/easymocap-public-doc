---
layout: default
title: Wild + multiple sparse
parent: Calibration
grand_parent: Quick Start
nav_order: 210
---

# Wild + multiple sparse

- **When use this:** sparse cameras, hard to calibrate for colmap;
- **Idea:** Use an extra phone to record the scene.
- Here you can find the [example data](http://gofile.me/66p77/k9pINXqo2).

## Capture 

<div align="center">
    <img src="assets/wild-sparse-background1f.jpg" width="60%">
    <br>
    <sup>background</sup>
    <br>
    <img src="assets/wild-sparse-ground1f.jpg" width="60%">
    <br>
    <sup>ground</sup>
    <br>
    <video width="60%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="assets/wild-sparse-scan.mp4" type="video/mp4">
    </video>
    <br>
    <sup>scan</sup>
</div>

Place the data as follows:

```bash
<calib_data>
├── background1f
│   ├── images
│   └── scan.mp4
└── ground1f
    └── images
```

## Calibration

### 1. Detect the chessboard

```bash
# detect the chessboard
python3 apps/calibration/detect_chessboard.py ${root}/ground1f --out ${root}/ground1f/output --pattern 9,6 --grid 0.1
# check the chessboard detection
python3 apps/annotation/annot_calib.py ${root}/ground1f --annot chessboard --mode chessboard
```

### 2. Calibrate by colmap

```bash
python3 apps/calibration/calib_static_dynamic_by_colmap.py ${root}/background1f ${root}/colmap --colmap ${colmap} --step 4
# check with colmap
${colmap} gui --database_path ${root}/colmap/database.db --image_path ${root}/colmap/images --import_path ${root}/colmap/sparse/0
```

### 3. Align to the chessboard

```bash
python3 apps/calibration/align_colmap_ground.py ${root}/colmap/sparse/0 ${root}/colmap/align --plane_by_chessboard ${root}/ground1f --prefix static/
```