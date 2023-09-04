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

{: .note }
Please check [EasyMoCap v0.3](../develop/develop.html) for more details.

# Demo for Motion Capture
## Demo on multiple calibrated cameras

The example dataset can be download from [01_triangulate/street_dance.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/street_dance
emc --data config/datasets/mvimage.yml --exp config/mv1p/detect_triangulate_fitSMPL.yml --root ${data} --subs_vis 07 01 05 03
```

The results can be found in `output/detect_triangulate_fitSMPL`.

<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../develop/assets/02_fitsmpl_output.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured outdoors using 9 smartphones.</sup>
</div>


{: .note }
Our method only takes 30 seconds to optimize the SMPL model of 800 frames. As rendering the results takes the longest time, you can add flag ` --skip_vis` to skip this.

## Demo on monocular videos

The example dataset can be download from [03_fitmono/internet-rotate.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/internet-rotate
emc --data config/datasets/svimage.yml --exp config/1v1p/hrnet_pare_finetune.yml --root ${data} --ranges 0 500 1 --subs 23EfsN7vEOA+003170+003670
```


<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../develop/assets/03_fitmono_smpl.mp4" type="video/mp4">
    </video>
    <br>
    <sup>The raw video is from <a href="https://www.youtube.com/watch?v=23EfsN7vEOA">Youtube</a>.</sup>
</div>

## Demo on monocular+mirror videos

Download example dataset [here](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/EZQDFJ-m3gNKiu1lMHMinK4BhsfKOBnCPngEL9mR0OmwZg?e=O5yUo0) and extract the dataset.


```bash
data=<path/to/data>
python3 apps/demo/mocap.py ${data} --work mirror --fps 30 --vis_scale 0.5
```

<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/mirror-test-youtube.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Videos come from <a href="https://www.youtube.com/watch?v=hVDPS-f6K5o">Youtube</a>.</sup>
</div>

# Demo for Novel View Synthesis

## Demo for NeuralBody


Download example dataset [here]() and extract the dataset.

```bash
data=/path/to/data
# Train Neuralbody:
python3 apps/neuralbody/demo.py ${data} --mode neuralbody --gpus 0,
# Render Neuralbody:
python3 apps/neuralbody/demo.py ${data} --mode neuralbody --gpus 0, --demo
```

Full step of motion capture and data preparation:
```bash
# motion capture
python3 apps/demo/mocap.py ${data} --work lightstage-dense-unsync --subs_vis 01 07 13 19 --disable_crop

```
<!-- ## Demo on static mesh

Download example mesh [here](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/Ea1qJYUnhcJLiQEZIHd6atYBKeYKVWNEHAw23dpAGNKQwg?e=taa4KU) and extract the dataset.

```bash
# Render the example mesh `xuzhen`
data=/path/to/data
python3 apps/vis/render_mesh.py ${data}/meshes/xuzhen --start -110 --up x --num 180
# Extract the keypoints if you use your own renderer datasets

```

After this, run our code to recover the pose parameters.

```bash
python3 apps/demo/mocap.py ${data} --mode scan --mono --render_side
```

The results in `${data}/output-mono-scan/smplmesh/xuzhen.mp4`:
 -->


<!-- ## Demo on monocular Mirrored-Human datasets

Download demo dataset [here](xxx) and extract the dataset.

```bash
python3 apps/demo/mocap.py ${data} --work mirror --mono
```

Results can be found in `${data}/output-mirror`.

<div align="center">
    <video width="70%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="../videos/mocap-handr-k3d.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Input 3D keypoints(left) and output MANO mesh(right) without smoothing.</sup>
    <br>
    <sup>Data comes from <a href="https://mks0601.github.io/InterHand2.6M/">InterHand2.6M dataset</a>/test/Capture0/ROM04_RT_Occlusion.</sup>
</div>


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
</div> -->
<!-- 
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
``` -->