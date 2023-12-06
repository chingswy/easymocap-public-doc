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

## Format

Image `000000.jpg` has its annotation file `0000000.json`:
```bash
{
    'keypoints3d': [[x0, y0, z0], [x1, y1, z1], ..., ],
    'keypoints2d': [[u0, v0, c0], [u1, v1, c1], ..., ].
}
```
