---
layout: default
title: Prepare Your Object Detector
parent: Quick Start
nav_exclude: true
nav_order: 10
---

# Prepare Your Object Detector
{: .no_toc }

1. TOC
{:toc}
---

In this tutorial, we will show how to annotate and train an object detector for your custom objects.

## Install

```bash
mkdir -p 3rdparty && cd 3rdparty
git clone https://github.com/chingswy/yolov5.git
wget https://github.com/ultralytics/yolov5/releases/download/v6.1/yolov5m.pt
mv yolov5m.pt models/
```

## Annotate

Create bbox by drag and press `n`.

```bash
python3 scripts/postprocess/cvt_yolo.py ${data} /home/qing/DGPU/nas/datasets/soccer/objects --annot ball
```

## Config and Train YOLOv5

```bash
python3 train.py --img 640 --batch 16 --epochs 200 --data data/anyobject.yml --weights models/yolov5m.pt --name anyobject
```

## Extract Objects from Images

```bash
python3 apps/preprocess/extract_object2d.py ${data} --ckpt 3rdparty/yolov5/runs/train/anyobject/weights/best.pt --out object2d
```

## Train Your Human+Hand+Face Detector




