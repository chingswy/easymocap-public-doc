---
layout: default
title: Quick Start
nav_order: 2
has_children: true
---

# Quick Start
{: .no_toc }

1. TOC
{:toc}
---

## Demo on multiple calibrated cameras

Download our demo dataset [here](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/ESnS1ix5LtxMqV_MWXQJMM4BoxRt5NQ5RmkYo4d5iZueAQ?e=shtmUJ) and extract the dataset. If you want to run this code on your own dataset, see [Prepare Your MoCap Dataset](./prepare_mocap.md) for more details.

```bash
data=/path/to/dataset
python3 apps/demo/mocap.py ${data} --mode smplh-3d
```

The visualization results can be found in `${data}/output-smplh-3d/smplmesh.mp4`

<div align="center">
    <video width="49%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/mocap-feng-smplh.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video comes from our ZJU-MoCap dataset with 19 calibrated and synchronized cameras.</sup>
</div>

Optionally, you can change the mode for other models:

|Model|SMPL|MANO|
|:----:|:----:|:----:|
|Mode|vposer-3d|manol|
|Results|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/mocap-feng-vposer.mp4" type="video/mp4"></video>|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/mocap-feng-handl.mp4" type="video/mp4"></video>|


## Demo on monocular videos

Download demo dataset [here](../datasets/1v1p-test.zip) and extract the dataset.

```bash
data=/path/to/dataset
python3 apps/demo/mocap.py ${data} --mode smpl-robust --mono
```

<div align="center">
    <video width="49%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/1v1p-test-cxk.mp4" type="video/mp4">
    </video>
    <video width="49%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/1v1p-test-wa.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Videos come from <a href="https://www.youtube.com/watch?v=GLu5YwiAtC4">Youtube</a> and <a href="https://www.bilibili.com/video/BV12X4y1c7AD?p=1">Bilibili</a>.</sup>
</div>

## Demo on monocular Mirrored-Human datasets

## Demo on 3D hand keypoints

Download demo dataset [here](../datasets/ROM04_RT_Occlusion.zip) and extract the dataset.

```bash
data=/path/to/ROM04_RT_Occlusion
python3 apps/fit/run_mocap.py ${data} --mode handr-kpts3d
```

Results can be found in `${data}/output-handr-kpts3d`.

<div align="center">
    <video width="70%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/mocap-handr-k3d.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Input 3D keypoints(left) and output MANO mesh(right) without smoothing.</sup>
    <br>
    <sup>Data comes from <a href="https://mks0601.github.io/InterHand2.6M/">InterHand2.6M dataset</a>/test/Capture0/ROM04_RT_Occlusion.</sup>
</div>

## Demo for Neuralbody

Prepare data:

```bash
python3 apps/postprocess/write_vertices.py ${data}/output-vposer-3d/smpl ${data}/output-vposer-3d/vertices --cfg_model ${data}/output-vposer-3d/cfg_model.yml --mode vertices
```

```bash
data=/path/to/data
# Train Neuralbody:
python3 apps/neuralbody/demo.py ${data} --mode neuralbody --gpus 0,
# Render Neuralbody:
python3 apps/neuralbody/demo.py ${data} --mode neuralbody --gpus 0, --demo
```

You can replace the mode `neuralbody` to `aninerf`

```bash
data=/path/to/data
# Train Animatable-NeRF:
python3 apps/neuralbody/demo.py ${data} --mode aninerf --gpus 0,
# Render Animatable-NeRF:
python3 apps/neuralbody/demo.py ${data} --mode aninerf --gpus 0, --demo
```