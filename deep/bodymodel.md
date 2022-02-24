---
layout: default
title: Body Model
parent: Development
nav_order: 1
---

# Body Model

{: .no_toc }

1. TOC
{:toc}
---


### parameter `Rh`

Original SMPL model use the first 3-dim of poses to represent the body orientation, instead we use an extra `Rh` and fill the first 3-dim with zero.

## SMPL+H
|full pose|[0, 3) | [3, 60) | [60, 63)| [63, 66) | [66, 66+45) | [66+45, 66+45+45)|
|----|:----:|:----:|:----:|:----:|:----:|:----:|
|meaning| rot| poses|       wrist L  |    wrist R | poses L  |   poses R |

## MANO left + right

This model is composed with MANO(left) and MANO(right). The poses parameter means:

|full pose|[0, 3) | [3, 48) | [48, 51)| [51,96) |
|----|:----:|:----:|:----:|:----:|
|meaning|       rot L  |   poses L    |   rot R  |   poses R |
