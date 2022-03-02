---
layout: default
title: mv1p
parent: Quick Start
nav_order: 1
---

# mv1p
{: .no_toc }

1. TOC
{:toc}
---

## Prepare dataset

### Test on ZJU-MoCap

Download our demo dataset [here]() and extract the dataset.

### Test on your own dataset

See [Prepare Your MoCap Dataset](./prepare_mocap.md) for more details.

## Run the demo code

```bash
data=/path/to/dataset
python3 apps/demo/mocap.py ${data}
```

## Check the visualization results

The visualization results can be found in `${data}/output-smpl-3d/smplmesh.mp4`

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

## :bug: Step-by-step debug

If everything works well, you can skip this. 

If something bad happened, you should check the process step-by-step.

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

Make sure that:

### 3. Run the triangulation code

```bash
python3 apps/fit/triangulate1p.py --cfg_data config/data/mv1p.yml --opt_data args.path ${data} args.out ${data}/output-keypoints3d --cfg_exp config/recon/mv1p-total.yml
```

### 4. Check the triangulation results

TODO

### 5. Run the fitting code

```bash
python3 apps/fit/run_mocap.py ${data} --name smpl-3d
```

### 6. Check the fitting results

<!-- report for 3D keypoints:
it reports the MPJPE error without root alignment.

report for smooth terms: -->
