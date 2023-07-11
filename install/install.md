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

### 2023.06.30 Update

`py39` + `cu116` + `torch 1.12.0`

```bash
git clone https://github.com/zju3dv/EasyMocap.git
conda create -n easymocap python=3.9 -y
conda activate easymocap
wget -c https://download.pytorch.org/whl/cu116/torch-1.12.0%2Bcu116-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torch-1.12.0+cu116-cp39-cp39-linux_x86_64.whl
wget -c https://download.pytorch.org/whl/cu116/torchvision-0.13.0%2Bcu116-cp39-cp39-linux_x86_64.whl
python3 -m pip install ./torchvision-0.13.0+cu116-cp39-cp39-linux_x86_64.whl
python -m pip install -r requirements.txt
pip install spconv-cu116
# install pyrender if you have a screen
python3 -m pip install pyrender
python setup.py develop
```

## 


## Prepare SMPL models

Download and prepare the needed models as follows. If you just use SMPL model, you can place the `smplv1.1.0` here.

To download the SMPL model go to this(version 1.1.0) project website and register to get access to the downloads section. After the downloading, place and extract it at `data/bodymodels/`:

```bash
data/bodymodels
└── SMPL_python_v.1.1.0
    └── smpl
        ├── __init__.py
        ├── models
        │   ├── basicmodel_f_lbs_10_207_0_v1.1.0.pkl
        │   ├── basicmodel_m_lbs_10_207_0_v1.1.0.pkl
        │   └── basicmodel_neutral_lbs_10_207_0_v1.1.0.pkl
        └── smpl_webuser
```

Other models are optional.

```bash
./data/bodymodels
├── FLAME2020
│   ├── flame_dynamic_embedding.npy
│   ├── FLAME_FEMALE.pkl
│   ├── FLAME_MALE.pkl
│   ├── FLAME_NEUTRAL.pkl
│   ├── flame_static_embedding.pkl
│   └── Readme.pdf
├── manov1.2
│   ├── MANO_LEFT.pkl
│   └── MANO_RIGHT.pkl
├── smplhv1.2
│   ├── female
│   ├── info.txt
│   ├── LICENSE.txt
│   ├── male
│   └── neutral
├── SMPL_python_v.1.1.0
│   └── smpl
└── vposer_v02
    ├── snapshots
    ├── V02_05.log
    └── V02_05.yaml
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
You can install EasyMocap to your current PyTorch environment. Most versions are supported. You can find all versions [here](https://download.pytorch.org/whl/torch_stable.html)

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
wget -c https://download.pytorch.org/whl/cu101/torch-1.7.1%2Bcu101-cp37-cp37m-linux_x86_64.whl
wget -c https://download.pytorch.org/whl/cu101/torchvision-0.8.2%2Bcu101-cp37-cp37m-linux_x86_64.whl
python3 -m pip install ./torch-1.7.1+cu101-cp37-cp37m-linux_x86_64.whl
python3 -m pip install ./torchvision-0.8.2+cu101-cp37-cp37m-linux_x86_64.whl
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
