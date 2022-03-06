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

You can install EasyMocap to your current PyTorch environment.

Create a conda environment and activate it.

```bash
conda create -n easymocap python=${PYVERSION} -y
conda activate easymocap
```


For cuda 10.0:
```bash
python3 -m pip install torch-1.4.0+cu100-cp37-cp37m-linux_x86_64.whl
pip install https://download.pytorch.org/whl/cu100/torchvision-0.5.0%2Bcu100-cp37-cp37m-linux_x86_64.whl
```

For cuda 10.1:
```bash
conda create -n easymocap python=3.7 -y
conda activate easymocap
python3 -m pip install torch==1.7.1+cu101 torchvision==0.8.2+cu101
```


For cuda11.1+Python3.9+torch1.9.1 (newest version when writing this):
```bash
conda create -n easymocap python=3.9 -y
conda activate easymocap
wget -c https://download.pytorch.org/whl/cu111/torch-1.9.1+cu111-cp39-cp39-linux_x86_64.whl
wget -c https://download.pytorch.org/whl/cu111/torchvision-0.10.1%2Bcu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install torch-1.9.1+cu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torchvision-0.10.1+cu111-cp39-cp39-linux_x86_64.whl
```

Then setup the EasyMocap

```bash
python3 setup.py develop
```
