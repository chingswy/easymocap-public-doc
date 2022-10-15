---
layout: default
title: Detect the chessboard
parent: Calibration
grand_parent: Quick Start
nav_order: 10000
---

# Detect the chessboard

## ChArco

```bash
python3 apps/calibration/detect_charuco.py ${root}/ba --mode sparse --squareLength 0.1 --aruco_len 0.0714
python3 apps/annotation/annot_calib.py ${root}/ba --annot chessboard --mode chessboard --pattern 5,3
```

|||
|----|----|
|--mode||
|--squareLength| the length of the square (unit meter)|


## Mannual

```bash
python3 apps/calibration/create_marker.py ${root}/background1f --N 4 --N_group 4
python3 apps/annotation/annot_mv_points.py ${root}/background1f
```

