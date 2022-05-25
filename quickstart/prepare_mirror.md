---
layout: default
title: Prepare Your Mirrored-Human Dataset
parent: Quick Start
nav_order: 5
---

# Prepare Your Mirrored-Human Dataset
{: .no_toc }

1. TOC
{:toc}
---


After this step, you can reconstruct the results in one step or step-by-step.

## One step reconstruction

```bash
xxx
```

The rendered results will be saved at `${data}/output-mirror/smplmesh/`.

If some bug occurs, you should run this algorithm step-by-step and check the results of each step.

## Detect and track the human

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
python3 apps/preprocess/extract_track.py ${data}
```

Process failure tracking:

**case 1:** tracking failed because wrong clip, you should re-clip this sequence:

```bash
python3 scripts/preprocess/reclip.py ${data} --start 0 --end <right_end_frame> --delete
```

This script will auto create a new folder and copy the images and annotations to the new folder. `--delete` flag will help you to delete the origina folder.


## Fitting SMPL

```bash
python3 apps/demo/mocap.py ${data} --mode mirror --mono
```
