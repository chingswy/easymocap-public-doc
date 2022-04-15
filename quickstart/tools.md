---
layout: default
title: Useful tools
parent: Quick Start
nav_order: 102
---

# Useful tools
---

### extract images from videos: `apps/preprocess/extract_image.py`

```bash
python3 apps/preprocess/extract_image.py ${data}
```

Extra flags:

|flag|type||
|----|----|----|
|--image|str|output directory(default `images`)|
|--ffmpeg|str|path to ffmpeg(default `ffmpeg`)|
|--transpose|int|transpose for ffmepeg(default -1, for clockwise)|

### copy and sample dataset: `scripts/preprocess/copy_dataset.py`

```bash
python3 scripts/preprocess/copy_dataset.py /path/to/input /path/to/output
```

Extra flags:

|flag|type||
|----|----|----|
|--start|int|start frame(default 0)|
|--end|int|end frame(default None)|
|--step|int|sample step(default 1)|
|--scale|float|resize image with scale(default 1)|

## Export vertices

```bash
python3 apps/postprocess/write_vertices.py ${data}/output-vposer-3d/smpl ${data}/output-vposer-3d/vertices --cfg_model ${data}/output-vposer-3d/cfg_model.yml --mode vertices
```

## Export triangle mesh

```bash
python3 apps/postprocess/write_vertices.py ${data}/output-vposer-3d/smpl ${data}/output-vposer-3d/mesh --cfg_model ${data}/output-vposer-3d/cfg_model.yml --mode mesh
```
