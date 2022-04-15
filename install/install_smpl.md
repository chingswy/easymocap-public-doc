---
layout: default
title: Prepare SMPL models
parent: Install
nav_order: 1
---


# Prepare SMPL models

{: .no_toc }

1. TOC
{:toc}
---

After we build EasyMocap v0.1, some models were updated. So you should make sure you have registered and downloaded the newest model.

## SMPL model

To download the *SMPL* model go to [this](http://smpl.is.tue.mpg.de)(version 1.1.0) project website and register to get access to the downloads section. After the downloading, place and extract it at `data/bodymodels/`:

```bash
data/bodymodels
└── SMPL_python_v.1.1.0
    └── smpl
        ├── __init__.py
        ├── models
        │   ├── basicmodel_f_lbs_10_207_0_v1.1.0.pkl
        │   ├── basicmodel_m_lbs_10_207_0_v1.1.0.pkl
        │   └── basicmodel_neutral_lbs_10_207_0_v1.1.0.pkl
        └── smpl_webuser
```

To check the model, please [install](install_vis3d.md#install-open3d) and use our 3D visualization tool:

```bash
python3 apps/vis3d/vis_smpl.py --cfg config/model/smpl.yml
```

## MANO + SMPL+H

To download the *SMPL+H* model go to [this project website](http://mano.is.tue.mpg.de) and register to get access to the downloads section. Download the newest [mano model (version 1.2)](https://psfiles.is.tuebingen.mpg.de/downloads/mano/mano_v1_2-zip) and place it into `data/bodymodels/manov1.2`. Download the newest [SMPL+H model](https://psfiles.is.tuebingen.mpg.de/downloads/mano/smplh-tar-xz)

```bash
data/bodymodels/
├── manov1.2
│   ├── MANO_LEFT.pkl
│   └── MANO_RIGHT.pkl
└── smplhv1.2
    ├── female
    │   └── model.npz
    ├── info.txt
    ├── LICENSE.txt
    ├── male
    │   └── model.npz
    └── neutral
        └── model.npz
```

To check the model, please use our 3D visualization tool:

```bash
# test the MANO model
python3 apps/vis3d/vis_smpl.py --cfg config/model/mano.yml
# test the SMPL+H model
python3 apps/vis3d/vis_smpl.py --cfg config/model/smplh.yml
```

## FLAME

TODO: Download

```bash
data/bodymodels/FLAME2020
├── flame_dynamic_embedding.npy
├── FLAME_FEMALE.pkl
├── FLAME_MALE.pkl
├── FLAME_NEUTRAL.pkl
├── flame_static_embedding.pkl
└── Readme.pd
```

To check the model, please use our 3D visualization tool:

```bash
python3 apps/vis3d/vis_smpl.py --cfg config/model/flame.yml
```

## SMPL-X

To download the *SMPL-X* model go to [this project website](https://smpl-x.is.tue.mpg.de) and register to get access to the downloads section. 

Download the [SMPL-X v1.1](https://download.is.tue.mpg.de/download.php?domain=smplx&sfile=models_smplx_v1_1.zip).

**TODO**

## VPoser

Register to `SMPL-X` project [page](https://smpl-x.is.tue.mpg.de) and download [VPoser v0.2](https://download.is.tue.mpg.de/download.php?domain=smplx&sfile=V02_05.zip).

```bash
data/bodymodels/vposer_v02
├── snapshots
│   ├── V02_05_epoch=08_val_loss=0.03.ckpt
│   └── V02_05_epoch=13_val_loss=0.03.ckpt
├── V02_05.log
└── V02_05.yaml
```

Test the model:

```bash
python3 apps/vis3d/vis_smpl.py --cfg config/model/smpl_vposer.yml
python3 apps/vis3d/vis_smpl.py --cfg config/model/smplh_vposer.yml
```

## Adam

TODO