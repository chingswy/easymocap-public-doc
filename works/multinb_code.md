---
layout: default
title: Code
parent: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
grand_parent: Works
nav_order: 3
---

# Code Tutorial

In this tutorial, we will show how to make a novel view synthesis with fantasy effects from sparse multi-view videos.

## Capture

Capture the videos with multiple cameras, rounghly synchronize them. Here we show the [example data](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/EUrwsDgin4JKlxtsXY_qOcUBozki-kUY65-9BOvd2-AzbQ?e=OOVqCF).

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

### Clip1

We play the frame from 0 to 40. We set the view from 0 to 80. In this clip, we render the object as the `object_keys`. Then, we freeze the time and view. We zoom the scene by scale the intrinsinc parameters.

```python
start:
  frame: [0, 40, 1]
  view: [0, 80, 2]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
zoomin:
  frame: [40, 41, 1]
  view: [80, 81, 1]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
  steps: 60
  effect: zoom
  effect_args:
    scale: [1., 2.]
    cx: [1., 1.]
    cy: [1., 1.]
```

{% include_relative video.html source="multinb-code/clip1.mp4" title="clip1" width="60%" %}

### Clip2

Then we render the bullet time after zooming in and zoom out by change the `scale` from `2` to `1`.

```python
rotate:
  frame: [40, 41, 1]
  view: [80, 200, 1]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
  effect: none
  effect_args:
    use_previous_K: True
zoomout:
  frame: [40, 41, 1]
  view: [200, 201, 1]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
  steps: 60
  effect: zoom
  effect_args:
    scale: [2., 1.]
    cx: [1., 1.]
    cy: [1., 1.]
```

{% include_relative video.html source="multinb-code/clip2.mp4" title="clip2" width="60%" %}

### Clip3

Besides traditional bullet time effect, our method can control the motion of each person. Here we keep all people static at `frame 40` and make a duplicate of `human_3`. The parameter `scale_occ` makes the duplicate transparent.

```yml
frozen1:
  frame: [40, 200, 2]
  view: [200, 201, 1]
  object_keys: ["ground_@{'frame': 40}", 'ball_0', "human_3_@{'scale_occ': 0.2}", "human_0_@{'frame': 40}", "human_1_@{'frame': 40}", "human_2_@{'frame': 40}", "human_3_@{'frame': 40}", "human_4_@{'frame': 40}", "human_5_@{'frame': 40}"]
frozen2:
  frame: [199, 39, -2]
  view: [200, 201, 1]
  object_keys: ["ground_@{'frame': 40}", 'ball_0', "human_3_@{'scale_occ': 0.2}", "human_0_@{'frame': 40}", "human_1_@{'frame': 40}", "human_2_@{'frame': 40}", "human_3_@{'frame': 40}", "human_4_@{'frame': 40}", "human_5_@{'frame': 40}"]
```

{% include_relative video.html source="multinb-code/clip3.mp4" title="clip3" width="60%" %}

### Clip4

Then we can play the motion and focus on the logo `SIGGRAPH` by zooming in.

```yml
normal:
  frame: [40, 65, 1]
  view: [200, 250, 2]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
bullet:
  frame: [65, 66, 1]
  view: [250, 490, 1]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
# 5. zoom in , vanish
zoomin2:
  frame: [65, 66, 1]
  view: [490, 491, 1]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
  steps: 60
  effect: zoom
  effect_args:
    scale: [1., 1.5]
    cx: [1., 0.7]
    cy: [1., 1.]
```

{% include_relative video.html source="multinb-code/clip4.mp4" title="clip4" width="60%" %}

### Clip5

Finally, we show the disappear effect by setting the key of selected people.

```yml
disappear3:
  frame: [65, 200, 1]
  view: [490, 491, 1]
  object_keys: [ground, human_0, human_1, human_2, human_3, human_4, human_5, ball_0]
  effect: disappear
  effect_args:
    key: ['human_1', 'human_2', 'human_5']
    use_previous_K: True
```

{% include_relative video.html source="multinb-code/clip5.mp4" title="clip5" width="60%" %}


## Demo for multi-objects

### 1. Get the object detections

If your object can not be detected with common object detectors, please annotate some data and train a custom yolo.

```bash
python3 train.py --img 640 --batch 16 --epochs 200 --data data/anyobject.yml --cfg models/yolov5m.yaml --weights /nas/share/yolo/yolov5m.pt --name object
```

Edit the `data/anyobject.yml`:

```yaml
# Train/val/test sets as 1) dir: path/to/imgs, 2) file: path/to/imgs.txt, or 3) list: [path/to/imgs1, path/to/imgs2, ..]
path: /nas/home/shuaiqing/object  # dataset root dir
train: images  # train images (relative to 'path') 128 images
val: images  # val images (relative to 'path') 128 images
# test:  # test images (optional)

# Classes
nc: 1  # number of classes
names: ['object'] # class names
```

### 2. Detect and Triangulate the detections

