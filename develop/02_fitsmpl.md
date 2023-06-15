---
layout: default
title: Fit SMPL
parent: Develop
nav_order: 2
---

{: .no_toc }

1. TOC
{:toc}
---

## Try the code

The example dataset can be download from [01_triangulate/street_dance.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/street_dance
emc --data config/datasets/mvimage.yml --exp config/mv1p/detect_triangulate_fitSMPL.yml --root ${data} --subs_vis 07 01 05 03
```

The results can be found in `output/detect_triangulate_fitSMPL`.

<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/02_fitsmpl_output.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured outdoors using 9 smartphones.</sup>
</div>

## Basic Method

Our method utilizes the SMPL[^smpl] (Skinned Multi-Person Linear) parametric model. It minimizes the distance between the keypoints of the SMPL model and the triangulated keypoints, as well as incorporates temporal smoothness loss for SMPL parameters and prior loss for SMPL pose parameters. By jointly optimizing the SMPL parameters for all frames, we achieve temporally consistent results.

## Step-by-step Explanation

### stages

The keypoint detection and triangulation parts are reused from the content of [01_triangulate](./01_triangulate.md). Here, we will mainly focus on describing the optimization process that occurs after triangulating all frames. First, we load the SMPL model and then construct the SMPL parameters. Through a multi-stage optimization approach, we optimize different parameters in each stage to obtain the final result.

```yaml
...
  at_final:
    load_body_model: # Load SMPL model
      module: myeasymocap.io.model.SMPLLoader
      args:
        model_path: models/pare/data/body_models/smpl/SMPL_NEUTRAL.pkl #
        regressor_path: models/J_regressor_body25.npy
    init_params: ... # initialize the SMPL parameters
    fitShape: ... # Fit the SMPL shape by 3D limbs
    init_RT: ... # Initialize the body rotation and translation
    refine_poses: ... # Optimize the poses
      # ...
      args:
        optimize_keys: [poses, Rh, Th]
        loss:
          k3d: ... # 3D keypoints distance
          smooth: ... # smooth term
          prior: ... # use GMM as pose prior
    write: ... # write the results
    render_ground: ... # render the SMPL with a ground
    make_video: ...
```

<!-- 
1. Single-frame operations
   1. Triangulate each frame, referring to the single-frame operation of task0
2. Global operations
   1. Obtain the human body's motion posture based on multi-frame 3d keypoints. Refer to the global operation of task3
3. Processing output
   1. Visualize the results of each frame

### Parameter tuning:

1. During single-frame processing, 3D keypoints were obtained through multi-view 2D keypoints. Therefore, in the optimization process, the main loss used is the distance between 3D keypoints. And because the 3D keypoints obtained by triangulation are quite accurate, L2 regularization can be used directly.

Preliminary tests using only 3D keypoints as Loss show that the human body's posture can be optimized to the desired position, but the posture can be quite distorted.

2. Add a prior loss to constrain the human body's posture. As can be seen from the results, the effect of posture has basically reached expectations.

3. We do not use Init loss here. That is, do not constrain the distance between the current posture and the initial posture, because the initial posture here is set to the default all zeros. But for something like task3, which provides an initial posture, you can choose to add this constraint.
 -->

## Fit MANO

The example dataset can be download from [01_triangulate/412-hand.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/412-hand
emc --data config/datasets/mvimage.yml --exp config/mv1p/detect_hand_triangulate_fitMANO.yml --root ${data} --subs_vis 0 1 2
```

<div align="center">
    <video width="60%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="./assets/02_fitsmpl_mano.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video are captured using 3 USB cameras.</sup>
</div>


## Reference

[^smpl]: Loper, Matthew, et al. "SMPL: A skinned multi-person linear model." ACM transactions on graphics (TOG) 34.6 (2015): 1-16.