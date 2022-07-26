---
layout: default
title: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
parent: Works
nav_order: 1
has_children: true
---

# Novel View Synthesis of Human Interactions From Sparse Multi-view Videos

{: .no_toc }

[arXiv(coming soon)](http://example.com/){: .btn .btn-blue }
[Code(coming soon)](http://example.com/){: .btn .btn-purple }

<div align="center">
    <video width="95%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_soccer1-6.mp4" type="video/mp4">
    </video>
    <br>
    <div> Given sparse multi-view videos of human performers, our approach is able to generate high-fidelity novel views and accurate instance masks even for crowded scenes. This scene is captured by 8 GoPro cameras.</div>
</div>

## Results on ZJUMoCap

<table cellspacing="0">
    <thead>
    </thead>
    <tbody id="demo">
      <tr>
        <td>
          <video width="99%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_boxing2.mp4" type="video/mp4">
          </video>
        </td>
        <td>
          <video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_basketball_disappear.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
      <tr>
        <td>
          <video width="99%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_handstand.mp4" type="video/mp4">
          </video>
        </td>
        <td>
          <video width="100%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_juggle.mp4" type="video/mp4">
          </video>
        </td>
      </tr>
    </tbody>
</table>


## Results in the wild

<div align="center">
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_soccer1-yuang.mp4" type="video/mp4">
    </video>
    <br>
    <video width="80%" playsinline="" autoplay="autoplay" loop="loop" preload="" muted=""><source src="multinb/demo_soccer1-beijia.mp4" type="video/mp4">
    </video>
    <br>
    <sup>Video comes from 8 GoPro cameras.</sup>
</div>

<!-- 
```bash
# training
python3 apps/neuralbody/demo.py ${data} --mode soccer1_yuang --gpus 0,1,2,3
# render the demo
python3 apps/neuralbody/demo.py ${data} --mode soccer1_yuang --gpus 0,1,2,3 --demo
# training
python3 apps/neuralbody/demo.py ${data} --mode soccer1_beijia --gpus 0,1,2,3
# render the demo
python3 apps/neuralbody/demo.py ${data} --mode soccer1_beijia --gpus 0,1,2,3 --demo
``` -->

<!-- ## Failure Cases

Consider the technical components of our work, we may fail in such cases: -->

## Limitations and future work

Currently, the proposed approach is limited to the setting of multiple human performers, only balls as objects, a simple background and a calibrated camera array. As future work, the system can be enhanced in several ways to handle more general settings. 

1. Recovering the human interaction from moving cameras or even a monocular video can be further investigated. 
2. More general objects can be handled by tracking the 6DoF
poses with object pose trackers. 
3. If offline scanning of the background is available, the rendering quality of the background can be further improved.

## Related Works
There are lots of wonderful works that inspired our work:

- [NeuralBody](https://github.com/zju3dv/neuralbody)
- [STNeRF](https://github.com/DarlingHang/st-nerf)

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

We would like to thank Haian Jin for the work in processing the instance segmentation.

We thank Zhengdong Hong's advice for generating the visualizations.

Special thanks to the Women’s campus football team of Zhejiang University and Beijia Chen.
