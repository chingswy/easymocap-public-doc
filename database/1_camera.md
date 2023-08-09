---
layout: default
title: Camera Parameters
parent: Database Format
nav_order: 1
mathjax: true
---

# Calibration
{: .no_toc }

1. TOC
{:toc}
---

## Camera Parameters

Intrisic parameter contains `K`, `dist`.

$$
K = \begin{bmatrix}
f_x & 0 & c_x \\
0 & f_y & c_y \\
0 & 0 & 1
\end{bmatrix},
$$

$$
\mathbf{dist}=(k_1, k_2, p_1, p_2, k_3).
$$

The definition of `dist` can be found in [OpenCV](https://docs.opencv.org/4.x/d4/d94/tutorial_camera_calibration.html),

Extrinsic parameter contains `R`,`T`.

$$
X_{cam} = R X_{world} + T.
$$

{: .note }
The metric of `T` must be `meter` in all of our codes.


## File Format

The file format is following [OpenCV format](https://docs.opencv.org/master/dd/d74/tutorial_file_input_output_with_xml_yml.html). We use `intri.yml` and `extri.yml` to store the camera parameters.

In each file, `names` records all the camera names, and `K_{name}`, `dist_{name}`, `R_{name}`, `T_{name}` records the parameters of each camera.

```yaml
names:
  - "01"
  - "03"
K_01: !!opencv-matrix
  rows: 3
  cols: 3
  dt: d
  data: [2272.816, 0.000, 1255.278, 0.000, 2269.930, 729.021, 0.000, 0.000, 1.000]
dist_01: !!opencv-matrix
  rows: 1
  cols: 5
  dt: d
  data: [0.057, -0.047, 0.002, -0.002, 0.000]
K_03: !!opencv-matrix
  rows: 3
  cols: 3
  dt: d
  data: [2272.816, 0.000, 1255.278, 0.000, 2269.930, 729.021, 0.000, 0.000, 1.000]
dist_03: !!opencv-matrix
  rows: 1
  cols: 5
  dt: d
  data: [0.057, -0.047, 0.002, -0.002, 0.000]
```

In `extri.yml`, `R_{name}` is the rotation vector, and `T_{name}` is the translation vector. `Rot_{name}` is the rotation matrix.

```yaml
names:
  - "01"
R_01: !!opencv-matrix
  rows: 3
  cols: 1
  dt: d
  data: [1.258, -1.292, 1.178]
Rot_01: !!opencv-matrix
  rows: 3
  cols: 3
  dt: d
  data: [-0.021, -1.000, -0.005, -0.087, 0.007, -0.996, 0.996, -0.021, -0.087]
T_01: !!opencv-matrix
  rows: 3
  cols: 1
  dt: d
  data: [0.453, 1.048, 4.957]
```

## Read and write camera

Read the camera of EasyMocap format:

```python
from easymocap.mytools.camera_utils import read_cameras
# path/intri.yml, path/extri.yml
path = 'xxx' 
cameras = read_cameras(path)
```

Write the camera of EasyMocap format:

```python
from easymocap.mytools.camera_utils import write_cameras
# cameras: dict
camera_00 = {
    'K': np.eye(3),
    'dist': np.zeros(5),
    'R': np.eye(3),
    'T': np.zeros(3),
}
camera_01 = {
    'K': np.eye(3),
    'dist': np.zeros(5),
    'R': np.eye(3),
    'T': np.zeros(3),
}
cameras = {
    '00': camera_00,
    '01': camera_01,
}
write_cameras(path, cameras)
```

More details can be found at `easymocap/mytools/camera_utils.py`=>`write_camera`, `read_camera` functions.

## Examples of converting camera parameters

- Convert Human3.6M dataset: [scripts/dataset/pre_h36m_camera.py](https://github.com/zju3dv/EasyMocap/blob/master/scripts/dataset/pre_h36m_camera.py)
- Convert Panoptic dataset: [scripts/dataset/pre_panoptic.py](https://github.com/zju3dv/EasyMocap/blob/master/scripts/dataset/pre_panoptic.py)
- Convert HI4D dataset: [scripts/dataset/pre_hi4d.py](https://github.com/zju3dv/EasyMocap/blob/master/scripts/dataset/pre_hi4d.py)

