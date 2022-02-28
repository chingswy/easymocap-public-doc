---
layout: default
title: Prepare for instance segmentation
parent: Install
nav_order: 2
---

# Instance segmentation

## schp

```bash
git clone https://github.com/PeikeLi/Self-Correction-Human-Parsing.git
cd Self-Correction-Human-Parsing
conda install ninja
python3 -m pip install scikit-image
python3 -m pip install networks
# install detectron2
python -m pip install detectron2 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cu111/torch1.9/index.html
```