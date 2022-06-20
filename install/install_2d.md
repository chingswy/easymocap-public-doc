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

Download model weight of HRNet

## Install MediaPipe

