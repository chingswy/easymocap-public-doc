---
layout: default
title: Triangulate
parent: Develop
nav_order: 1
---

{: .no_toc }

1. TOC
{:toc}
---

## Try the code

The example dataset can be download from [01_triangulate/street_dance.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/street_dance
emc --data config/datasets/mvimage.yml --exp config/mv1p/detect_triangulate.yml --root ${data} --subs_vis 07 01 05 03
```

The results can be found in `output/detect_triangulate`.

<div align="center">
    <video width="60%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/01_triangulate_output.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured outdoors using 9 smartphones.</sup>
</div>

## Basic Method

Our approach utilizes YOLO for person detection, employs HRNet[^hrnet] for 2D keypoint estimation, and performs multi-view triangulation to obtain accurate 3D keypoints of the human body.

## Step-by-step Explanation

In this step, I will demonstrate the implementation under the code framework: 
- read 2D keypoints and camera parameters from the data; 
- multi-view triangulation, visualization; 
- result smoothing.

### dataset

We use a yml file for control, here we used `config/datasets/mvimage.yml`,

```yaml
module: myeasymocap.datasets.mv1p.MVDataset
args:
  root: TO_BE_FILLED
  subs: []  # used views, default all views
  subs_vis: ['01'] # visualized views
  ranges: [0, 10000, 1]
  read_image: True
  reader:
    images:
      root: images
      ext: .jpg
    image_shape:
      root: images
      ext: .jpg
    cameras:
      root: ''
```

In this file, we first declare the module we are using, `module`, the syntax here is equivalent to using `from myeasymocap.datasets.mv1p import MVDataset` in Python, and the parameters needed when this class is instantiated are defined in `data_args`.

Please refer to the corresponding source code file for the data read into this function.

### stages

After obtaining the data, we can operate on the data. The most common scenario is to process a segment of video data, so the framework design defaults to operations with a time dimension.

We also use a yml file for control, the corresponding experimental configuration is in `config/mv1p/detect_triangulate.py`

```yaml
# The 'module' declares the multi-stage class used
module: myeasymocap.stages.basestage.MultiStage
args:
  output: output/detect_triangulate
  at_step: # This declares the operations to be performed on each frame of data
    detect: ... # detect the human by YOLO
    vis_det: ... # visualize the detection results
    keypoints2d: ... # estimate the 2D keypoints by HRNet
    vis2d: ... # visualize the human keypoints
    triangulate: ... # In this task, we only perform triangulation
    visualize: ... # Visualize the reprojection of each frame
  at_final: # This declares the operations that will be performed on all frames after completing the operations on each frame
    smooth: ... # Here we perform the smoothing of the skeleton
    write: ... # write the 3D keypoints
    make_video: ...
```

Multi-stage process control mainly includes two parts: operations corresponding to each frame and operations for all frames.

- Operations for each frame consist of an ordered dictionary, given each frame's data, the program will execute the modules defined here in order. In this task, because there is only one triangulate module, only one is written.
- For each module, we still use the `module` + `args` method to declare. In addition, for parameter passing, we define `key_from_data` to represent the variables passed into this module. `key_keep` is used to record the information that needs to be saved from the input `data` for subsequent sequential processing or visualization.
- The return values of each module in the `at_step` stage, and the selected return values in `key_keep`, will all be collected as input to the `at_final` stage.
- Similarly in `at_final`, we define a smooth module, this module has a parameter of smoothing window size, and the variable it needs to use during the call is `keypoints3d`.
- After smoothing, we save the `keypoints3d` data. Here, a `Write` module is called, which needs to specify the output path, and the result will be saved in the specified path.

The code for each module can be found in the Python file defined by `module`. Similarly, this definition also supports the introduction of modules from third-party libraries.

### command line

After understanding the above two parts, you can run our program in the command line

```bash
emc --data config/datasets/mvimage.yml --exp config/mv1p/detect_triangulate.yml --root ${data} --subs_vis 07 01 05 03
```

Here, `--data` is used to specify the above data configuration, and `--exp` is used to specify the corresponding experimental configuration. The reason for using two configurations to record is that the same data can be used for different experiments.

We utilize the --root command to set the data path and the --subs_vis command to specify the viewpoints for visualization. Additional command-line parameters can be viewed by running emc -h.

## Hand

Our method can be easily extended to different keypoint configurations, such as handling hand data in a similar manner. The specific workflow can be found in the corresponding experimental file. In this case, we use mediapipe to obtain 2D keypoints of the hand. You can install it by running pip install mediapipe==0.10.

The example dataset can be download from [01_triangulate/412-hand.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/412-hand
emc --data config/datasets/mvimage.yml --exp config/mv1p/detect_hand_triangulate.yml --root ${data} --subs_vis 0 1 2
```

<div align="center">
    <video width="60%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/01_triangulate_hand.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured using 3 USB cameras.</sup>
</div>

Here, we have defined an interface module for mediapipe. This module is responsible for reading images and using mediapipe to detect their 2D keypoints.

```yaml
    detect:
      module: myeasymocap.backbone.mediapipe.hand.MediaPipe
      key_from_data: [images, imgnames]
      args:
        ckpt: models/mediapipe/hand_landmarker.task
```

## Object

TODO


## Reference

[^hrnet]: Sun, Ke, et al. "Deep high-resolution representation learning for human pose estimation." Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition. 2019.