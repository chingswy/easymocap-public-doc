---
layout: default
title: Keypoints Definition
parent: Quick Start
nav_order: 100
---

# Keypoints Definition
{: .no_toc }

1. TOC
{:toc}
---

## Extract keypoints

Quick overview for selecting the model:

|Model|Install|Comment|
|----|----|----|
|mediapipe|easy install|only support 1 person|
|yolo+hrnet|medium|on feet keypoints|
|openpose|hard|multi person+feet|

In most common usage, we use `body25 format` of OpenPose[^openpose] as our standard keypoints. Outputs of other method like `HRNet`[^hrnet], `mediapipe`[^mediapipe] will be converted to `body25 format`.

For each image, we record its 2D pose in a `json` file. For an image at `root/images/1/000000.jpg`, the 2D pose willl store at `root/annots/1/000000.json`. The content of the annotation file is:

```bash
{
    "filename": "images/0/000000.jpg",
    "height": <the height of image>,
    "width": <the width of image>,
    "annots:[
        {
            'personID': 0, # ID of person
            'bbox': [l, t, r, b, conf],
            'keypoints': [[x0, y0, c0], [x1, y1, c1], ..., [xn, yn, cn]],
            'area': <the area of bbox>
        },
        {
            'personID': 1, # ID of person
            'bbox': [l, t, r, b, conf],
            'keypoints': [[x0, y0, c0], [x1, y1, c1], ..., [xn, yn, cn]],
            'area': <the area of bbox>
        }
    ]
}
```

For each `keypoints`, `[x0, y0, c0]` means the (`x`, `y`) position in image and `confidence` of this keypoints. It's supposed to be `0` if this keypoint is invisible.

If you use hand and face, the annot is defined as:
```bash
{
    "personID": i,
    "bbox": [l, t, r, b, conf],
    "keypoints": [[x0, y0, c0], [x1, y1, c1], ..., [xn, yn, cn]],
    "bbox_handl2d": [l, t, r, b, conf],
    "bbox_handr2d": [l, t, r, b, conf],
    "bbox_face2d": [l, t, r, b, conf],
    "handl2d": [[x0, y0, c0], [x1, y1, c1], ..., [xn, yn, cn]],
    "handr2d": [[x0, y0, c0], [x1, y1, c1], ..., [xn, yn, cn]],
    "face2d": [[x0, y0, c0], [x1, y1, c1], ..., [xn, yn, cn]]
}
```
### YOLOv4+HRNet

Download the model from their official websites: [HRNet](https://drive.google.com/drive/folders/1hOTihvbyIxsm5ygDpbUuJ7O_tzv4oXjC)

```bash
data/models
????????? pose_hrnet_w48_384x288.pth
????????? yolov4.weights
```

No other requirements are needed, just run:

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
```

### OpenPose

OpenPose[^openpose] can detect the human body, hand, facial and foot keypoints, you should install this follow their [tutorial](https://github.com/CMU-Perceptual-Computing-Lab/openpose).


```bash
openpose=<path/to/openpose/installation>
# detect the body and feet keypoints
python3 apps/preprocess/extract_keypoints.py ${data} --mode openpose --openpose ${openpose}
# detect the hand and face if needed
python3 apps/preprocess/extract_keypoints.py ${data} --mode openpose --openpose ${openpose} --hand --face
```

### Mediapipe

Install it with pip:

```
python3 -m pip install mediapipe
```

Run the detection of full body:

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode mp-holistic
```

### YOLOv4+Openpose

This mode will first perform human detection[^yolov4] and second run the OpenPose on the cropped images.

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode openposecrop --openpose ${openpose}
```

### YOLOv4+HRNet+Openpose

This mode will first perform human detection and second run the HRNet on the cropped images. Finnally use OpenPose to detect the feet keypoints.

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet & python3 apps/preprocess/extract_keypoints.py ${data} --mode feetcrop --openpose ${openpose} --force
```

## Keypoints definition
### OpenPose

|name||
|----|----|
|body|![body](https://raw.githubusercontent.com/CMU-Perceptual-Computing-Lab/openpose/master/.github/media/keypoints_pose_25.png) |
|hand| ![hand](https://raw.githubusercontent.com/CMU-Perceptual-Computing-Lab/openpose/master/.github/media/keypoints_hand.png) |
|face| ![face](https://raw.githubusercontent.com/CMU-Perceptual-Computing-Lab/openpose/master/.github/media/keypoints_face.png) |

### Mediapipe

|name||
|----|----|
|body|![body](https://google.github.io/mediapipe/images/mobile/pose_tracking_full_body_landmarks.png) |
|hand| ![hand](https://google.github.io/mediapipe/images/mobile/hand_landmarks.png) | 
|face| ![face](../images/dataset/mediapipe-facemesh.jpg) |

### SMPL

|name||
|----|----|
|SMPL[^smpl]|![body](../images/dataset/SMPL.png) |


[^smpl]: Loper, Matthew, et al. "SMPL: A skinned multi-person linear model." ACM transactions on graphics (TOG) 34.6 (2015): 1-16.


[^openpose]: Cao, Z., Hidalgo, G., Simon, T., Wei, S.E., Sheikh, Y.: Openpose: real-time multi-person 2d pose estimation using part affinity fields. arXiv preprint arXiv:1812.08008 (2018)

[^hrnet]: Sun, Ke, et al. "Deep high-resolution representation learning for human pose estimation." Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition. 2019.

[^mediapipe]: Lugaresi, Camillo, et al. "Mediapipe: A framework for building perception pipelines." arXiv preprint arXiv:1906.08172 (2019).

[^yolov4]: Bochkovskiy, Alexey, Chien-Yao Wang, and Hong-Yuan Mark Liao. "Yolov4: Optimal speed and accuracy of object detection." arXiv preprint arXiv:2004.10934 (2020).