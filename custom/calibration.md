---
layout: default
title: Calibration
parent: Prepare Your MoCap Dataset
grand_parent: Prepare
nav_order: 1
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
