---
layout: default
title: Prepare Your Monocular Dataset
parent: Quick Start
nav_order: 4
---

# Prepare Your Monocular Dataset
{: .no_toc }

1. TOC
{:toc}
---

## Capture

Record the video by yourself or [download from YouTube](./capture_youtube.md)

## Prepare SPIN models

Download pretrained SPIN model [here](http://visiondata.cis.upenn.edu/spin/model_checkpoint.pt) and place it to `data/models/spin_checkpoint.pt`.

Fetch the extra data [here](http://visiondata.cis.upenn.edu/spin/data.tar.gz) and place the `smpl_mean_params.npz` to `data/models/smpl_mean_params.npz`.

```bash
mkdir -p data/models
wget -O data/models/spin_checkpoints.pt http://visiondata.cis.upenn.edu/spin/model_checkpoint.pt
wget -c http://visiondata.cis.upenn.edu/spin/data.tar.gz
# data/models/smpl_mean_params.npz
```

## Extract keypoints

See [prepare keypoints](./keypoints.md#extract-keypoints)


<!-- ## Public Dataset

### HumanNeRF

HumanNeRF provides 3 Internet videos.

```bash
for vid in 0ORaAnJYROg gEpJDE8ZbhU ANwEiICt7BM;do python3 scripts/dataset/download_youtube.py ${vid} --database data/datasets/humannerf; done
# extract images
python3 apps/preprocess/extract_image.py ${data}
# annot the clip
python3 apps/annotation/annot_clip.py ${data}
```

We manually clip this dataset. You can place this to `${data}/clips.json`

```python
{
    "0ORaAnJYROg": [[4705,4955]],
    "ANwEiICt7BM": [[2315,2615]],
    "gEpJDE8ZbhU": [[1500, 1650]]
}
```

Run the mocap:
```bash
python3 apps/demo/mocap.py ${data} --work internet
``` -->

<!-- 
### DeepCap
Download and place the data:

```bash
├── Antonia
│   └── images0.avi
├── Lan
│   ├── images0.avi
│   ├── images1.avi
│   └── images2.avi
├── Magdalena
│   ├── images0.avi
│   ├── images1.avi
│   └── images2.avi
├── Marc
│   ├── images0.avi
│   └── images1.avi
├── monocularCalibrationBM.calibration
├── monocularCalibration.calibration
└── monocularCalibrationPhone.calibration
```

Apply this to other sequence too. -->
