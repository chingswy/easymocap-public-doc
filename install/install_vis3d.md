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

Install pyrender in a computer with a screen:
```bash
python3 -m pip install pyrender
```

Install pyrender in a server:

```bash
mkdir -p 3rdparty
cd 3rdparty
sudo apt update
sudo wget https://github.com/mmatl/travis_debs/raw/master/xenial/mesa_18.3.3-0.deb
sudo dpkg -i ./mesa_18.3.3-0.deb || true
sudo apt install -f
git clone https://github.com/mmatl/pyopengl.git
python3 -m pip install ./pyopengl
echo "export PYOPENGL_PLATFORM=osmesa" >> ~/.zshrc
export PYOPENGL_PLATFORM=osmesa
```

## Install Open3D

```bash
python3 -m pip install open3d==0.14.1
```

## Install PyTorch3D