---
layout: default
title: Realtime Demo
parent: Quick Start
nav_order: 1
has_toc: true
nav_exclude: true
---

# Realtime Demo
{: .no_toc }

- TOC
{:toc}
---

In this tutorial, we show how to build a real-time mocap system with EasyMocap.

## 0. Setup your cameras and calibrate them

In our tutorial, we use 3 usb cameras and place them in left, middle, and right of the desktop.

```bash
python3 apps/camera/realtime_display.py --cfg_cam config/camera/usb-logitech.yml --display
```

There will be three windows display in the screen.

```bash
data=dataset/desktop/calib
# record the videos
python3 apps/camera/realtime_display.py --cfg_cam config/camera/usb-logitech.yml --display --num 1800 --out ${data}
# calibration the camera
python3 apps/calibration/calib_onestep.py ${data} --grid 0.03 --pattern 11,8
```

<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/desktop-calib.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Calibration example.</sup>
</div>

{: .note }
- You should keep the chessboard static and visible in all views at the start.
- You should fix the focals of all cameras.

After the calibration, check the camera parameters and visualize.

```bash
python3 apps/calibration/check_calib.py ${data} --mode cube --out ${data} --grid_step 0.1 --write --show
```

<div align="center">
    <img src="../images/calib/desktop_calib_cube.jpg" width="80%">
    <br>
    <sup>Check the calibration results. The cube will be placed on the origin of the world coordinate.</sup>
</div>

## 1. Check the keypoints detection tool

## 2. Run the demo for left hand

### step 1. open the detector

```bash
python3 apps/camera/detect_server.py --cfg_cam config/camera/usb-logitech.yml --host 0.0.0.0:8888 --cfg_det config/camera/mediapipe-hand.yml --opt_cam args.params ${data}
```

### step 2. open the visualization

```bash
python3 apps/vis/vis_server.py --cfg config/vis3d/o3d_scene_manol.yml host 0.0.0.0 port 9999 block True
```

### step 3. run the main code

```bash
python3 apps/fit/triangulate1p.py --cfg_data config/recon/socket_mv1p.yml --cfg_exp config/recon/fit_manol.yml --vis3d localhost:9999 --det2d localhost:8888
```

## 2. Run the demo for body

### step 1. open the detector

```bash
python3 apps/camera/detect_server.py --cfg_cam config/camera/usb-logitech.yml --host 0.0.0.0:8888 --cfg_det config/camera/mediapipe-body.yml --opt_cam args.params ${data}
```

### step 2. open the visualization

```bash
python3 apps/vis/vis_server.py --cfg config/vis3d/o3d_scene_smpl.yml host 0.0.0.0 port 9999 block True
```

### step 3. run the main code

```bash
python3 apps/fit/triangulate1p.py --cfg_data config/recon/socket_mv1p.yml --cfg_exp config/recon/fit_smpl.yml --vis3d localhost:9999 --det2d localhost:8888
```
