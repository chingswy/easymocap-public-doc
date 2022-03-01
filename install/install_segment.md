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
# install detectron2
python -m pip install detectron2 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cu111/torch1.9/index.html
```

Given a dataset as EasyMocap format, extract the instance segmentation with this script:

```bash
python3 extract_multi.py ${data}
```

Results can be found in `data/`
