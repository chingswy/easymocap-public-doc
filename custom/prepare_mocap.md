---
layout: default
title: Prepare Your MoCap Dataset
parent: Prepare
nav_order: 1
---


## Extract images from videos

```bash
python3 apps/preprocess/extract_image.py ${data}
```

## Extract keypoints from images

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
```

## Public Dataset

### AMA

```bash
data=/path/to/ama/D_handstand
python3 scripts/dataset/pre_ama.py ${data} --image
```

Apply this to other sequence too.