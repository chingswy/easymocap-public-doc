---
layout: default
title: Prepare for instance segmentation
parent: Install
nav_order: 3
---

# Instance segmentation

## SCHP: Self Correction for Human Parsing

SCHP is an out-of-box human parsing representation extractor.

Given an environment of EasyMocap, we can install this code as following:

```bash
cd 3rdparty
git clone https://github.com/chingswy/Self-Correction-Human-Parsing.git
cd Self-Correction-Human-Parsing
conda install ninja
python3 -m pip install scikit-image
python3 -m pip install networks
```

### Install detectron2

Install detectron2 according to your cuda version and torch version. For example cu111+torch.19:

```
python -m pip install detectron2 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cu111/torch1.9/index.html
```

### Download the models

Place the related models in a folder:

```bash
/path/to/model/schp
├── detectron2_maskrcnn_cihp_finetune.pth
├── exp_schp_multi_cihp_global.pth
└── exp_schp_multi_cihp_local.pth
```

### Usage

Given a dataset as EasyMocap format, extract the instance segmentation with this script:

```bash
python3 extract_multi.py ${data} --ckpt_dir /path/to/models
```

Results can be found in `data/`

{ :.warning }
This code will generate some very big(>100G) outputs. If you don't have enough space in `data/`, please add ` --tmp /path/to/tmp`