---
layout: default
title: Studio + multiple sparse
parent: Calibration
grand_parent: Quick Start
nav_order: 105
---

# Studio + multiple sparse

- **When use this:** sparse cameras, hard to initialize for colmap;
- **Idea:** Chessboard for initialization. Merge feature points from different frames and BA together.
- Here you can find the [example data](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/EWsM-G3mEi5Gt-Xs7a7bJqIBqd_1FK__9_HmFCvvBGrPTg?e=IsZG9h).

## Initialization

```bash
├── ground1f
│   └── images
└── intri
    └── images
```

## Capture 

<div align="center">
    <img src="assets/studio-sparse-intri.jpg" width="50%">
    <br>
    <sup>intri</sup>
    <br>
    <img src="assets/studio-sparse-ground1f.jpg" width="50%">
    <br>
    <sup>ground</sup>
</div>

## Run

```bash
# detect the chessboard
python3 apps/calibration/detect_chessboard.py ${root}/intri --out ${root}/intri/output --pattern 9,6 --grid 0.1
# detect the chessboard
python3 apps/calibration/detect_chessboard.py ${root}/ground1f --out ${root}/ground1f/output --pattern 9,6 --grid 0.1 --check
```

```bash
# Run this if auto-detect failed
python3 apps/annotation/annot_calib.py ${root}/ground1f --mode chessboard --annot chessboard
```


Calibrate:

```bash
# calibrate the intrinsic
python3 apps/calibration/calib_intri.py ${root}/intri
# calibrate the extrinsic
python3 apps/calibration/calib_extri.py ${root}/ground1f --intri ${root}/intri/output/intri.yml
```

Check the calibration

```bash
python3 apps/calibration/check_calib.py ${root}/ground1f --out ${root}/ground1f --mode cube --write
```

Check `${root}/ground1f/cube`, or run with flag `--show` to visualize.

<div align="center">
    <img src="assets/studio-sparse-check-cube.jpg" width="50%">
    <br>
    <sup>cube</sup>
</div>


{: .note }
Previous step is enough for camera calibration. The next step is for the advanced developers.


Capture a static scene with multiple person and calibrate them with colmap.

<div align="center">
    <img src="assets/studio-sparse-human1f.jpg" width="50%">
    <br>
    <sup>cube</sup>
</div>


```bash
python3 apps/calibration/calib_sparse_by_colmap.py ${root}/human519 --init ${root}/ground1f --out /mnt/data2/shuai/calib-zjumocap --colmap ${colmap}
```

# Studio + multiple sparse videos

- **When use this:** sparse cameras, hard to initialize for colmap;
- **Idea:** Merge features from multiple frames => calibrate with colmap => scale and align with chessboard 
- Here you can find the [example data]().

```bash
${root}
├── 506
├── 508
└── ground1f
```

## Run colmap

```bash
python3 apps/calibration/calib_pycolmap.py ${root} ${root}/calib --share_camera --step 100 --seqs 506 508
$colmap gui --database_path ${root}/calib/merged/database.db --image_path ${root}/calib/merged/images --import_path ${root}/calib/merged/sparse/0
```

## Align with the chessboard

```bash
python3 apps/calibration/detect_chessboard.py ${root}/ground1f --out ${root}/ground1f/output --pattern 9,6 --grid 0.1
python3 apps/calibration/align_colmap_ground.py ${root}/calib/merged/sparse/0 ${root}/colmap-align --plane_by_chessboard ${root}/ground1f --scale2d 0.5
cp ${root}/colmap-align/*.yml ${root}/506
cp ${root}/colmap-align/*.yml ${root}/508
```
