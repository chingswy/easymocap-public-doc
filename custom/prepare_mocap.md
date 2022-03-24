<!--
 * @Date: 2022-03-07 18:52:52
 * @Author: Qing Shuai
 * @Mail: s_q@zju.edu.cn
 * @LastEditors: Qing Shuai
 * @LastEditTime: 2022-03-24 15:51:01
 * @FilePath: /easymocap-public-doc/custom/prepare_mocap.md
-->
---
layout: default
title: Prepare Your MoCap Dataset
parent: Prepare
nav_order: 1
---


## Extract images from videos

```bash
python3 apps/preprocess/extract_image.py ${data}
```

## Extract keypoints from images

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
```

## Public Dataset

### AMA

```bash
data=/path/to/ama/D_handstand
python3 scripts/dataset/pre_ama.py ${data} --image
```

Apply this to other sequence too.