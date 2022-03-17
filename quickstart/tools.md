---
layout: default
title: Useful tools
parent: Quick Start
nav_order: 2
---

# Useful tools
{: .no_toc }

1. TOC
{:toc}
---

Copy dataset:
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
