---
layout: default
title: Fit SMPL to Monocular Videos
parent: Develop
nav_order: 3
---

# Fit SMPL to Monocular Videos

{: .no_toc }

1. TOC
{:toc}
---

相比于多视角数据，单视角数据有其独特的优势：采集非常容易，不需要标定，不需要同步，不需要多个摄像头。因此，单视角数据在实际应用中有着广泛的应用场景。本文档将介绍如何使用EasyMocap对单视角数据进行处理。

相比于多视角数据，单视角数据的拟合的原理是：基于单目的human pose estimation的网络作为初值，通过优化的方式，使其考虑2D keypoints观测与时序的一致性，从而得到更好的SMPL参数。


- `dataset` 这里我们定义了一个对应于单目的数据的dataset，他只需要读取单张图像与对应的关键点信息。
- `at_step` 对于每一帧的处理，我们使用了一个data-driven的单目估计模型，作为身体的参数的初始估计
- `at_final` 完成了每一帧的估计之后，我们将组合所有帧的初始化SMPL估计结果、所有帧的2D关键点，一起联合优化。

