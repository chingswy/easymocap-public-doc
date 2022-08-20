---
layout: default
title: :bug:Debug
nav_order: 13
has_children: true
---

# :bug:Debug
{: .no_toc }

1. TOC
{:toc}
---

## MV1P

### 1. Check the datasets

Make sure that:

1. The dataset is synchronized
2. The 2D detections are almost right


```bash
# use the annotation tool to check the 2D keypoints
python3 apps/annotation/annot_keypoints.py ${data}
# check the dataset
python3 apps/fit/test_dataset.py --cfg_data config/data/mv1p.yml --opt_data args.path ${data} args.out ${data}/output-keypoints3d
```

### 2. Check the calibration

- Make sure that the unit of extrinsic parameter is `meter`.
- Use `check_calib.py` to visualize the camera:

```bash
# this command will plot a unit cube in the origin:
python3 apps/calibration/check_calib.py ${data} --out ${data} --mode cube --write --show
# this command will read and triangulate the keypoints of the human and project it to each views.
python3 apps/calibration/check_calib.py ${data} --out ${data} --mode human --write --show
```


### 3. Check the triangulation results

The results will be stored at `${data}/output-keypoints3d`

### 4. Check the output parameter

1. If the shape is abnormal, check the `shapes` parameters. 

### 5. Check the fitting with SMPL

```bash
# check only first 1 frames
python3 apps/demo/mocap.py ${data} --mode smpl-3d --ranges 0 1 1 --exp debug1
# check only first 10 frames
python3 apps/demo/mocap.py ${data} --mode smpl-3d --ranges 0 10 1 --exp debug10
# check only first 100 frames
python3 apps/demo/mocap.py ${data} --mode smpl-3d --ranges 0 100 1 --exp debug100
```

### 6. Check the fitting results

<!-- report for 3D keypoints:
it reports the MPJPE error without root alignment.

report for smooth terms: -->
