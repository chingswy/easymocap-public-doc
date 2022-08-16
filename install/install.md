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


Briefly, you can following our one-step [installation instructions](#install-easymocap-quickly). If you want to install the full package or install to you own environments, please see [installation instructions](#install-easymocap-step-by-step).


## Install EasyMocap Quickly

Make sure that you have installed `cuda11.1` and `conda`.

```bash
git clone https://github.com/zju3dv/EasyMocap.git
conda create -n easymocap python=3.9 -y
conda activate easymocap
wget -c https://download.pytorch.org/whl/cu111/torch-1.9.1%2Bcu111-cp39-cp39-linux_x86_64.whl
wget -c https://download.pytorch.org/whl/cu111/torchvision-0.10.1%2Bcu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torch-1.9.1+cu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torchvision-0.10.1+cu111-cp39-cp39-linux_x86_64.whl
python -m pip install -r requirements.txt
# install pyrender if you have a screen
python3 -m pip install pyrender
python setup.py develop
```


## Install EasyMocap Step-by-Step

Briefly, to run the demo, you should at least install:
1. [PyTorch](#install-pytorch)
2. [pyrender for visualization](./install_vis3d.md)
3. [human body prior](#install-human-body-prior)
4. [EasyMocap](#install-easymocap)

## Install EasyMocap

Then setup the EasyMocap

```bash
git clone https://github.com/zju3dv/EasyMocap.git
python3 -m pip install -r requirements.txt
python3 setup.py develop
```

## Install PyTorch

{: .note }
You can install EasyMocap to your current PyTorch environment. Most versions are supported.

Simply create a conda environment and activate it.

```bash
conda create -n easymocap python=3.9 -y
conda activate easymocap
python3 -m pip install torch torchvision
```

For cuda11.1+Python3.9+torch1.9.1:

```bash
conda create -n easymocap python=3.9 -y
conda activate easymocap
wget -c https://download.pytorch.org/whl/cu111/torch-1.9.1%2Bcu111-cp39-cp39-linux_x86_64.whl
wget -c https://download.pytorch.org/whl/cu111/torchvision-0.10.1%2Bcu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torch-1.9.1+cu111-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torchvision-0.10.1+cu111-cp39-cp39-linux_x86_64.whl
```

Check your cuda environment:
```bash
# export CUDA_VER=10.0
# export CUDA_VER=10.1
export CUDA_VER=11.4
export PATH=/usr/local/cuda-$CUDA_VER/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda-$CUDA_VER/lib64:$LD_LIBRARY_PATH
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


## Install human body prior

You can skip this if you don't use this module.

```bash
bash ./scripts/install/install_vposer.sh
```

---

## Other Modules

After this, if you want to use the different modules, you should install their corresponding requirements:

### NeuralBody


```bash
python3 -m pip install -r requirements_neuralbody.txt
python3 -m pip install spconv-cu111
# install pytorch3d when you want to use AniNerf
bash ./scripts/install/install_pytorch3d.sh
```