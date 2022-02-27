---
layout: default
title: mv1p
parent: Quick Start
nav_order: 1
---

# mv1p
{: .no_toc }

1. TOC
{:toc}
---




```bash
# triangulate the multi-view 2D detections
python3 apps/fit/triangulate1p.py --cfg_data config/data/mv1p.yml --opt_data args.path ${data} args.out ${data}/output-keypoints3d --cfg_exp config/recon/mv1p-total.yml
# copy the output to ${root}
cp -r ${data}/output-keypoints3d/keypoints3d ${data}
```


## Step-by-step debug

### 1. Check the datasets

```bash
python3 apps/fit/test_dataset.py --cfg_data config/data/mv1p.yml --opt_data args.path ${data} args.out ${data}/output-keypoints3d
```

### 2. Check the triangulation results

TODO

### 3. Check the fitting results

report for 3D keypoints:
it reports the MPJPE error without root alignment.

report for smooth terms:

TODO: It reports the velocity.
