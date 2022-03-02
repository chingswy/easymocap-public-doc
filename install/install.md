---
layout: default
title: Install
nav_order: 2
has_children: true
---

# Install
{: .no_toc }

1. TOC
{:toc}
---

Create a conda environment and activate it.

```bash
conda create -n easymocap python=3.7 -y
conda activate easymocap
```

You can install EasyMocap to your current PyTorch environment.

For cuda 10.0:
```bash
python3 -m pip install torch-1.4.0+cu100-cp37-cp37m-linux_x86_64.whl
pip install https://download.pytorch.org/whl/cu100/torchvision-0.5.0%2Bcu100-cp37-cp37m-linux_x86_64.whl
```

For cuda11.1:
```bash
python3 -m pip install torch-1.9.1+cu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torchvision-0.10.0+cu111-cp39-cp39-linux_x86_64.whl --no-deps
```