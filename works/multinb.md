---
layout: default
title: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
parent: Works
nav_order: 1
---

# Novel View Synthesis of Human Interactions From Sparse Multi-view Videos

{: .no_toc }

[arXiv(coming soon)](http://example.com/){: .btn .btn-blue }
[Code(coming soon)](http://example.com/){: .btn .btn-purple }

<div align="center">
    <video width="95%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_soccer1-6.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Given sparse multi-view videos of human performers, our approach is able to generate high-fidelity novel views and accurate instance masks even for crowded scenes. This scene is captured by 8 GoPro cameras.</sup>
</div>

## More Results

<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_soccer1-yuang.mp4" type="video/mp4">
    </video>
    <br>
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_soccer1-beijia.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video comes from 8 GoPro cameras.</sup>
</div>


<details markdown="block">
  <summary>
    Quick Start
  </summary>
  {: .text-delta }

```**bash**
# training
python3 apps/neuralbody/demo.py ${data} --mode soccer1_yuang --gpus 0,1,2,3
# render the demo
python3 apps/neuralbody/demo.py ${data} --mode soccer1_yuang --gpus 0,1,2,3 --demo
# training
python3 apps/neuralbody/demo.py ${data} --mode soccer1_beijia --gpus 0,1,2,3
# render the demo
python3 apps/neuralbody/demo.py ${data} --mode soccer1_beijia --gpus 0,1,2,3 --demo
```
</details>


## Failure Cases

Consider the technical components of our work, we may fail in such cases:

<!-- 1. 运动过快，导致无法三角化
2.  -->

## Limitation

More works can be done:

1. Model the exposure or white balance as a camera-dependent effect.
2. Model the background as a static NeRF captured with another moving camera.


## Related Works
There are lots of wonderful works that inspired our work:

- [NeuralBody]()
- [STNeRF]()

## Bibtex

```bash
@inproceedings{sun2022neuconw,
  title={Novel View Synthesis of Human Interactions from Sparse
Multi-view Videos},
  author={Shuai, Qing and Geng, Chen and Fang, Qi and Peng, Sida and Shen, Wenhao and Zhou, Xiaowei and Bao, Hujun},
  booktitle={SIGGRAPH Conference Proceedings},
  year={2022}
}
```

## Acknowledgement

The authors would like to acknowledge support from NSFC (No.
62172364).

We would like to thank Haian Jin for the work of processing the instance segmentation.

We thank Zhengdong Hong's advices for generating the visualizations.

Special thanks to Women’s campus football team of Zhejiang University and Beijia Chen.
