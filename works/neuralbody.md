---
layout: default
title: Tutorial for Neuralbody
parent: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
grand_parent: Works
nav_order: 3
---

# Tutorial for capturing your own datasets

In this tutorial, we show how to capture your datasets with multiple cameras.

This is the [example dataset before preprocessing] and the is the [example dataset after preprocessing].

You can compare it with your datasets.

## Capture and Calibrate

We recommend to calibrate as this [pipeline]().

## Motion Capture

```bash
# Reconstruct the human
python3 apps/demo/mocap.py ${data} --work mvmp-wild --ranges 0 300 1 --subs_vis 1 3 5 7 --pids 0 1 2 3 4 5
```

```bash
python3 apps/postprocess/write_vertices.py ${data}/output-smpl-3d/smpl ${data}/output-smpl-3d/vertices --cfg_model ${data}/output-smpl-3d/cfg_model.yml --mode vertices
python3 apps/postprocess/render.py ${data} --exp output-smpl-3d --mode instance-d0.05 --ranges 0 1400 1
```


<table cellspacing="0">
    <thead>
    </thead>
    <tbody id="demo">
      <tr>
        <td>Skeleton
        </td>
        <td>
          <video width="99%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/soccer1_6_keypoints.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
      <tr>
        <td>Mesh
        </td>
        <td>
          <video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/soccer1_6_smpl.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
      <tr>
        <td>Soccer
        </td>
        <td>
          <video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/soccer1_6_object.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
    </tbody>
</table>

## Training

```bash
python3 apps/neuralbody/demo.py --mode soccer1_6 --gpus 0,1,2,3 ${data}
```

## Rendering

```bash
python3 apps/neuralbody/demo.py--mode soccer1_6 --gpus 0,1,2,3 --demo ${data} 
```

The config for this scene can be found in `config/neuralbody/dataset/demo_soccer1_6.yml`. We explain this code and show how to perform scene editing step by step.

