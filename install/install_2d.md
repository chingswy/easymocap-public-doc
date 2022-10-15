---
layout: default
title: Prepare for Keypoints Detection
parent: Install
nav_order: 1
---

# Prepare for Keypoints Detection

{: .no_toc }

1. TOC
{:toc}
---

## Install OpenPose

Linux:

```bash
git clone https://github.com/CMU-Perceptual-Computing-Lab/openpose.git --depth 1
cd openpose
git submodule update --init --recursive --remote
sudo apt install libopencv-dev
sudo apt install protobuf-compiler libgoogle-glog-dev
sudo apt install libboost-all-dev libhdf5-dev libatlas-base-dev
mkdir build
cd build
cmake .. -DBUILD_PYTHON=true
make -j8
```

## Install Yolov4+HRNet

Download model weight of `yolov4`:

```bash
mkdir -p data/models
wget -c https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.weights
mv yolov4.weights data/models
```

Download `pose_hrnet_w48_384x288.pth` from (OneDrive)[https://1drv.ms/f/s!AhIXJn_J-blW231MH2krnmLq5kkQ]

## Install MediaPipe

