---
layout: default
title: Prepare Your MoCap Dataset
parent: Quick Start
nav_order: 3
---

# Prepare Your MoCap Dataset
{: .no_toc }

1. TOC
{:toc}
---

## Capture

## Extract keypoints

See [prepare keypoints](./keypoints.md#extract-keypoints)


## Public Dataset

### aist


### AMA

```bash
data=/path/to/ama/D_handstand
python3 scripts/dataset/pre_ama.py ${data} --image
```

Apply this to other sequence too.