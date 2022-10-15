---
layout: default
title: Wild + multiple sparse
parent: Calibration
grand_parent: Quick Start
nav_order: 210
---

# Wild + multiple sparse

- **When use this:** sparse cameras, hard to calibrate for colmap;
- **Idea:** Use an extra phone to record the scene.
- Here you can find the [example data](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/EWsM-G3mEi5Gt-Xs7a7bJqIBqd_1FK__9_HmFCvvBGrPTg?e=IsZG9h).

## Capture 

<div align="center">
    <img src="assets/wild-sparse-background1f.jpg" width="50%">
    <br>
    <sup>background</sup>
    <br>
    <img src="assets/wild-sparse-ground1f.jpg" width="50%">
    <br>
    <sup>ground</sup>
    <br>
    <img src="assets/studio-sparse-ground1f.jpg" width="50%">
    <br>
    <sup>ground</sup>
</div>


```bash
python3 apps/calibration/calib_static_dynamic_by_colmap.py ${root}/background1f ${root}/colmap --colmap ${colmap} --step 4
# check with colmap
${colmap} gui --database_path ${root}/colmap/database.db --image_path ${root}/colmap/images --import_path ${root}/colmap/sparse/0
```