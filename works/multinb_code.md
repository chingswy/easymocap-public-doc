---
layout: default
title: Code
parent: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
grand_parent: Works
nav_order: 1
---

# Code Tutorial

In this tutorial, we will show how to make a novel view synthesis with fantasy effects from sparse multi-view videos.

## Capture

Capture the videos with multiple cameras, rounghly synchronize them. Here we show the example data.

<table cellspacing="0">
    <thead>
    </thead>
    <tbody id="demo">
      <tr>
        <td>
          <video width="99%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/1.mp4" type="video/mp4">
          </video>
        </td>
        <td>
          <video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/3.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
      <tr>
        <td>
          <video width="99%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/5.mp4" type="video/mp4">
          </video>
        </td>
        <td>
          <video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb-code/7.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
    </tbody>
</table>

## Motion Capture

```bash
# Reconstruct the human
python3 apps/demo/mocap.py ${data} --work mvmp-wild --ranges 0 300 1 --subs_vis 1 3 5 7 --pids 0 1 2 3 4 5
# Reconstruct the object
python3 apps/demo/mocap.py ${data} --work object --ranges 0 300 1 --subs_vis 1 3 5 7
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
    </tbody>
</table>

## Training

```bash
python3 apps/neuralbody/demo.py ${data} --mode soccer1_6 --gpus 0,1,2,3
```

## Rendering

```bash
python3 apps/neuralbody/demo.py ${data} --mode soccer1_6 --gpus 0,1,2,3 --demo
```

