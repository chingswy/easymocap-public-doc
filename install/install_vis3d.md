---
layout: default
title: Prepare for visualization
parent: Install
nav_order: 2
---

# Prepare for visualization

{: .no_toc }

1. TOC
{:toc}
---

## Install Pyrender

Pyrender is used to visualized the mesh during fitting.

{: .note }
If you meet some errors like `pyglet.canvas.xlib.NoSuchDisplayException: Cannot connect to "None"`, you must run this code on a server. You should follow this tutorial.

Install pyrender in a computer with a screen:
```bash
python3 -m pip install pyrender
```

Install pyrender in a server:

1. Install osmesa with sudo

```bash
sudo apt update
sudo wget https://github.com/mmatl/travis_debs/raw/master/xenial/mesa_18.3.3-0.deb
sudo dpkg -i ./mesa_18.3.3-0.deb || true
sudo apt install -f
```

2. Install pyopengl

```bash
mkdir -p 3rdparty
cd 3rdparty
git clone https://github.com/mmatl/pyopengl.git
python3 -m pip uninstall pyopengl
python3 -m pip install ./pyopengl
# add osmesa to environment variable
echo "export PYOPENGL_PLATFORM=osmesa" >> ~/.zshrc
export PYOPENGL_PLATFORM=osmesa
```

{: .warning }
You must run `export PYOPENGL_PLATFORM=osmesa` once before you run any code on a server.

## Install Open3D

Open3D is used to perform realtime visualization and SMPL visualization with GUI. No need for this if you just run the fitting code.

We test the 3D visualization tools on Open3D==0.14.1.

```bash
python3 -m pip install -U pip # run this if pip can not find this version
python3 -m pip install open3d==0.14.1
```

## Install PyTorch3D
