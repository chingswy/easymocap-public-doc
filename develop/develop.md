---
layout: default
title: Develop
nav_order: 3
has_children: true
---

# Develop
{: .no_toc }

1. TOC
{:toc}
---

## Motivation

1. For beginners in the Mocap field, learn PyTorch programming by replicating the basic Mocap algorithms, and the basic principles of motion capture.
2. For MoCap researchers, you can learn how to standardize the addition of modules and implement new algorithms in EasyMoCap through this document. Focus directly on the development of the algorithm, without needing to repeatedly implement input/output operations and visualization.
3. For EasyMoCap users, you can preview some codes not included in the official version in this document.

## Structure

Our code consists of three main parts:

|Part||
|----|----|
|`dataset`|This part provides data for a specific time point, such as a single image or multiple images from different perspectives at that time point.|
|`at_step`|This part processes the data at each time point. For example, it estimates keypoints for a single frame or triangulates keypoints for the current frame.|
|`at_final`|This part performs post-processing on the entire dataset after iterating through all the data. This can include offline smoothing or fitting the SMPL model.|

## Start

We learn through a series of examples, each of which includes the corresponding data. You can download them and run the corresponding code.

### [1. Triangulate](./01_triangulate.html)

Start learning from the triangulation of single-person 2D keypoints from multiple perspectives.

|Body|Hand|
|----|----|
|<video width="90%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/01_triangulate_output.mp4" type="video/mp4"></video>|<video width="90%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/01_triangulate_hand.mp4" type="video/mp4"></video>|

### [2. Fit SMPL](./02_fitsmpl.html)

Fit a SMPL parametric model to 3D keypoints.

|Model|Output|
|----|----|
|SMPL|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/02_fitsmpl_output.mp4" type="video/mp4"></video>|
|MANO|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/02_fitsmpl_mano.mp4" type="video/mp4"></video>|

### [3. SMPLify](./03_fitsmpl_monocular.html)

Fit SMPL model to monocular 2D keypoint input.

|Model|Output|
|----|----|
|SMPL|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/03_fitmono_smpl.mp4" type="video/mp4"></video>|
|MANO|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/03_fitmono_anymano.mp4" type="video/mp4"></video>|
|Fixed MANO|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/03_fitmono_mano.mp4" type="video/mp4"></video>|

### [4. Multiple Person](./04_multiperson.html)

Fit SMPL model to multiple person from multi-view inputs.

|Model|Output|
|----|----|
|Ballet|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/04_ballet.mp4" type="video/mp4"></video>|
|Soccer|<video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/04_soccer1.mp4" type="video/mp4"></video>|

