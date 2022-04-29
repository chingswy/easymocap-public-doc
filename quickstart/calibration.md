---
layout: default
title: Calibration
parent: Quick Start
nav_order: 101
---

# Calibration
{: .no_toc }

1. TOC
{:toc}
---

## Format

For each multiple cameras dataset, you should have intrinsic parameter and extrinsic parameter. 

Intrisic parameter contains `K`, `dist` for each camera.

Extrinsic parameter contains `R`,`T` for each camera, where `RX + T` converts point `X` in world coordinate to camera coordinate.

An example of camera paramter can be found in [our demo dataset](../datasets/demo-feng.zip)

{: .note }
The metric of `T` must be `meter` in all of our codes.


## Read and write camera

```python
from easymocap.mytools.camera_utils import read_cameras, write_camera

# path/intri.yml, path/extri.yml
path = 'xxx' 
cameras = read_cameras(path)
write_camera(outdir, cameras)
```