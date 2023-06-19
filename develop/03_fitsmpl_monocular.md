---
layout: default
title: Monocular Videos
parent: Develop
nav_order: 3
---

{: .no_toc }

1. TOC
{:toc}
---

Compared to multi-view data, single-view data has its unique advantages: it is **easy to capture**, does not require calibration, synchronization, or multiple cameras. Therefore, single-view data finds wide applications in practical scenarios. This document will guide you on how to process single-view data using EasyMocap.

## Try the code

The example dataset can be download from [03_fitmono/internet-rotate.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/internet-rotate
emc --data config/datasets/svimage.yml --exp config/1v1p/hrnet_pare_finetune.yml --root ${data} --ranges 0 500 1 --subs 23EfsN7vEOA+003170+003670
```


<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/03_fitmono_smpl.mp4" type="video/mp4">
    </video>
    <br>
    <sup>The raw video is from <a href="https://www.youtube.com/watch?v=23EfsN7vEOA">Youtube</a>.</sup>
</div>

## Basic Idea

- **Initialize**: Use a network-based human pose estimation method to estimate the initial SMPL parameters.
- **Optimization**: Minimize the re-projection error and temporal smoothness error.

## Step-by-step Explanation

### dataset

Here, we define a dataset specifically for monocular data. It only requires reading individual images. The camera parameter is not required. We assume this is a static camera.

### at_step

- We use YOLOv5 and HRNet to detect and estimate the human pose. A simple tracking method is used to track the detected human.
- We use `PARE` to initialize the SMPL parameters.

### at_final

Once the estimation for each frame is completed, we combine the initial SMPL estimates from all frames with the 2D keypoints of all frames for joint optimization.

## Command Line

```bash
emc --data config/datasets/svimage.yml --exp config/1v1p/hrnet_pare_finetune.yml --root ${data} --ranges 0 500 1 --subs 23EfsN7vEOA+003170+003670
```

We use `--subs` to specify the selected video.


## Fit MANO to Monocular Videos

Similarly, we can fit a MANO model to monocular videos, and this extension is straightforward.

The example dataset can be download from [03_fitmono/hand.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

||Body|Hand|
|----|----|----|
|2D Keypoints|yolo+HRNet|2D Hand Network|
|Init|PARE|MANO Estimation Network|

More details can be found in `config/1v1p/hand_detect_finetune.yml`.

Running the code:

```bash
data=data/examples/hand
emc --data config/datasets/svimage.yml --exp config/1v1p/hand_detect_finetune.yml --root ${data} --ranges 0 1800 1 --subs video
```

<div align="center">
    <video width="60%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/03_fitmono_anymano.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured using one iPhone.</sup>
</div>

## Fit MANO to Fixed Hand Pose

**Motivation**: In scenarios where a hand is grasping an object without a CAD model, we can estimate the object's pose by estimating the hand's pose.

**Insight**: Even when the hand is occluded by the object, we can assume the hand's pose remains stationary. By optimizing a globally consistent pose, we can reduce the ambiguity of monocular cues and minimize errors introduced by occlusion.

The example dataset can be download from [03_fitmono/hand_fix_example.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

**Code**: We add this part into `at_final`:

```yaml
    mean_param:
      module: myeasymocap.operations.init.MeanShapes
      key_from_data: [params]
      args:
        keys: ['poses', 'shapes'] # Mean the poses and shapes
```

Running the code:

```bash
data=data/examples/3_Giuliano
emc --data config/datasets/svimage.yml --exp config/1v1p/fixhand.yml --root ${data} --ranges 0 1800 1
```

<div align="center">
    <video width="60%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/03_fitmono_mano.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured using one iPhone.</sup>
</div>