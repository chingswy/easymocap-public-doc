---
layout: default
title: NeuralBody
parent: Works
nav_order: 1
has_children: true
---

# Tutorial for capturing your own datasets

In this tutorial, we show how to capture your datasets with multiple cameras.

This is the [example dataset before preprocessing] and the is the [example dataset after preprocessing].

You can compare it with your datasets.

## Capture and Calibrate

Please check our calibration tutorial [here](../quickstart/calibration).

Assuming you have completed the data collection and calibration, you will obtain the following dataset:

- The `videos` folder contains synchronized videos from each camera
- The `images` folder contains synchronized images from each camera, named in the format of `%06d.jpg`, starting from 0. Please note that the following code mainly uses the image folder. Therefore, if you have obtained videos directly, you need to convert the videos into images first.
- `intri.yml` and `extri.yml` contain the intrinsic and extrinsic parameters of the cameras

```bash
313
├── images
│   ├── 01
│       └ %06d.jpg
│   ├── 02
│   ...
│   ├── 22
│   └── 23
├── extri.yml
├── intri.yml
└── videos
    ├── 01.mp4
    ├── 02.mp4
    ...
    ├── 22.mp4
    └── 23.mp4
```

## Keypoint Detection

We highly recommend using the official OpenPose model for key point detection as it includes body and foot points. If you use HRNet as the key point model, foot points will not be available. Please refer to the official documentation for installing OpenPose.

### 1. Using OpenPose for Keypoint Detection

To improve accuracy, we use YOLO for pre-detection to crop the detected individuals and then use OpenPose for key point detection.

```bash
# Use the yolov5x6 model for person detection
easymocap_tools extract_yolo ${data} annots --ckpt /nas/share/yolov5x6.pt --gpus 1
# Specify the CUDA devices to be used
export CUDA_VISIBLE_DECIECES=0
# Specify the path to your OpenPose installation, which should include the build folder with the compiled OpenPose results
export openpose=<path/to/your/openpose>
# Detect 2D keypoints in the cropped regions
python3 apps/preprocess/extract_keypoints.py ${data} --mode openposecrop --force
```


# Document in Chinese
## 创建你的数据集

假设你已经采集与标定完成了，那么你将获得如下的数据集：
- videos里包含每个相机的同步视频
- images里包含每个相机的同步图片，以`%06d.jpg`的格式命名，从0开始。注意，接下来的代码主要使用的都是图片文件夹，因此如果你直接获取的是视频，需要先将视频转换为图片
- `intri.yml`, `extri.yml`里包含相机的内参与外参

```bash
313
├── images
│   ├── 01
│   ├── 02
│   ...
│   ├── 22
│   └── 23
├── extri.yml
├── intri.yml
└── videos
    ├── 01.mp4
    ├── 02.mp4
    ...
    ├── 22.mp4
    └── 23.mp4
```

## 关键点检测

我们非常推荐你使用OpenPose官方的模型进行关键点检测，因为他包含了身体+脚的点。如果你使用HRNet作为关键点模型，那么将没有脚部的点。OpenPose的安装请参考官方文档。

### 1. 使用OpenPose来检测关键点

为了提高精度，我们使用的是yolo预先检测，将检测的人体进行crop，通过openpose来检测关键点。

```bash
# 使用yolov5x6模型来检测人体
easymocap_tools extract_yolo ${data} annots --ckpt /nas/share/yolov5x6.pt --gpus 1
# 指定使用的CUDA
export CUDA_VISIBLE_DECIECES=0,
# 指定使用的open pose的路径，该路径下需要包含build文件夹，里面是openpose的编译结果
export openpose=<path/to/your/openpose>
# 检测crop区域的2D关键点
python3 apps/preprocess/extract_keypoints.py ${data} --mode openposecrop --force
```

### 2. 使用HRNet来检测关键点

TODO

### 3. 可视化检查2D关键点

```bash
emc --data config/datasets/mv1p.yml --exp config/mv1p/vis_body_keypoints2d.yml --opt_data args.root /nas/ZJUMoCap/Part0/313 --opt_exp args.output output/vis-debug
```

## 前景分割



## 获得SMPL参数

## 获得前景分割

TODO

## 训练neural body

```bash
# copy the file to ${data}
cp -r output/vis-debug ${data}/output-smpl-3d
# extract the vertices
python3 apps/postprocess/write_vertices.py ${data}/output-smpl-3d/smpl ${data}/output-smpl-3d/vertices --cfg_model config/model/smpl.yml --mode vertices
```