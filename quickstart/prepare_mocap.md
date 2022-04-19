---
layout: default
title: Prepare Your MoCap Dataset
parent: Quick Start
nav_order: 3
---

# Prepare Your MoCap Dataset
{: .no_toc }

1. TOC
{:toc}
---

## Capture

## Extract keypoints

See [prepare keypoints](./keypoints.md#extract-keypoints)


## Public Dataset

### Panoptic Dataset

Download datasets, take `150821_dance1` as example:

```bash
python3 scripts/dataset/download_panoptic.py 150821_dance1
```

Extract the videos to images. This step may takes a lot of time as the videos is too large.

```bash
data=/nas/datasets/Panoptic/150821_dance1
python3 apps/preprocess/extract_image.py ${data}
```

Check the region of interest and copy the clips of interest, e.g. frame 160 - 460

```bash
python3 scripts/preprocess/copy_dataset.py ${data} ${data}/../150821_dance1_160_460 --start 160 --end 460
```

You can do this with our clip tool:

```bash
python3 apps/annotation/annot_clip.py ${data} --mv
python3 apps/annotation/annot_clip.py ${data} --mv --copy
```

### aist


### AMA

```bash
data=/path/to/ama/D_handstand
python3 scripts/dataset/pre_ama.py ${data} --image
```

Apply this to other sequence too.