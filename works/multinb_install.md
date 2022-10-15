---
layout: default
title: Install
parent: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
grand_parent: Works
nav_order: 1
---

# Install

### 0. Install Python + PyTorch

```bash
conda create -n easymocap python=3.9 -y
conda activate easymocap
wget -c https://download.pytorch.org/whl/cu111/torch-1.9.1%2Bcu111-cp39-cp39-linux_x86_64.whl
wget -c https://download.pytorch.org/whl/cu111/torchvision-0.10.1%2Bcu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torch-1.9.1+cu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torchvision-0.10.1+cu111-cp39-cp39-linux_x86_64.whl
```

### 1. Setup EasyMocap

```bash
python -m pip install -r requirements.txt
python setup.py develop
```

### 2. Setup NeuralBody

```bash
python3 -m pip install -r requirements_neuralbody.txt 
```
****
### Check

TODO