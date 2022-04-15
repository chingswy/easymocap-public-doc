---
layout: default
title: Prepare Your Object Detector
parent: Quick Start
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



使用鼠标标注一个物体的框，按n键新建。

按g键自动跟踪，跟踪过程中如果发现错误的框，按q停止自动跟踪。

## Config and Train YOLOv5

```bash
python3 train.py --img 640 --batch 16 --epochs 200 --data data/anyobject.yml --weights models/yolov5m.pt --name anyobject
```

## Extract Objects from Images


## Train Your Human+Hand+Face Detector




