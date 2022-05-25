---
layout: default
title: Calibration
parent: Quick Start
nav_order: 101
---

# Calibration
{: .no_toc }

1. TOC
{:toc}
---

## Format

For each multiple cameras dataset, you should have intrinsic parameter and extrinsic parameter. 

Intrisic parameter contains `K`, `dist` for each camera.

Extrinsic parameter contains `R`,`T` for each camera, where `RX + T` converts point `X` in world coordinate to camera coordinate.

An example of camera paramter can be found in [our demo dataset](../datasets/demo-feng.zip)

{: .note }
The metric of `T` must be `meter` in all of our codes.


## Read and write camera

```python
from easymocap.mytools.camera_utils import read_cameras, write_camera

# path/intri.yml, path/extri.yml
path = 'xxx' 
cameras = read_cameras(path)
write_camera(outdir, cameras)
```

## Step of calibrating LightStage system

```bash
# detect the chessboard
python3 apps/calibration/detect_chessboard.py ${data} --out ${data}/output --pattern 9,6 --grid 0.10
# check the annotation
python3 apps/annotation/annot_calib.py ${data} --annot chessboard --mode chessboard
ground=/nas/datasets/ZJUMoCap-v1/ground
ba=/nas/datasets/ZJUMoCap-v1/ba
python3 apps/calibration/calib_extri.py ${ground} --intri ${ba}/output/intri.yml
python3 apps/calibration/check_calib.py ${ground} --mode cube --out ${ground} --show --write
# BA RT
python3 apps/calibration/calib_ba_by_chessboard.py ${ba} --init ${ground} --out ${ba}/calib-base
```

If it's failed to detect chessboard in some frames, you can plot a box and press `e` to re-detect it.
