---
layout: default
title: FAQ
parent: :bug:Debug
nav_order: 1
---

# FAQ

> ImportError: cannot import name 'OSMesaCreateContextAttribs' from 'OpenGL.osmesa' (/home/qing/miniconda3/envs/easymocap/lib/python3.9/site-packages/OpenGL/osmesa/__init__.py)

Check [Install pyrender in a server:](https://chingswy.github.io/easymocap-public-doc/install/install_vis3d.html)

> ImportError: ('Unable to load OpenGL library', 'OSMesa: cannot open shared object file: No such file or directory', 'OSMesa', None)

In Linux, you should make sure that you have installed `osmesa`. See [Install osmesa with sudo](https://chingswy.github.io/easymocap-public-doc/install/install_vis3d.html)

> NoSuchDisplayException: Cannot connect to "None"

Run `export PYOPENGL_PLATFORM=osmesa`.

