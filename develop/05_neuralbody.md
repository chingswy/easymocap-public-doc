---
layout: default
title: Neural Body
parent: Develop
nav_order: 5
---

{: .no_toc }

1. TOC
{:toc}
---

In this section, you will learn how to utilize the results of motion capture to achieve 3D reconstruction of the human body and free viewpoint rendering. Our approach primarily relies on neuralbody, but similar methods such as aninerf can also be employed.

## Try the code

### Preprocess

We will render the previously generated SMPL results into instance maps and vertices.

```bash
data=<path/to/boxing>
mkdir -p ${data}/output-smpl-3d
cp -r output/boxing/smpl ${data}/output-smpl-3d
# convert the SMPL parameter to vertices
python3 apps/postprocess/write_vertices.py ${data}/output-smpl-3d/smpl ${data}/output-smpl-3d/vertices --cfg_model config/model/smpl.yml --mode vertices
# render the instance map
python3 apps/postprocess/render.py ${data} --exp output-smpl-3d --mode instance-d0.05 --ranges 0 200 1 --model config/model/smpl.yml
```

Check the dataset can be loaded rightly:

```bash
python3 apps/neuralbody/check_trainset.py --cfg config/neuralbody/dataset/multiview/lightstage.yml --opts split train data_share_args.root ${data}
```

### Train

### Render

