---
layout: default
title: Novel View Synthesis of Human Interactions From Sparse Multi-view Videos
parent: Works
nav_order: 2
has_children: true
---

# Novel View Synthesis of Human Interactions From Sparse Multi-view Videos

{: .no_toc }

[Paper](https://dl.acm.org/doi/pdf/10.1145/3528233.3530704){: .btn .btn-blue }
[Code](./multinb_code.md){: .btn .btn-purple }
[Dataset](https://github.com/zju3dv/EasyMocap#zju-mocap){: .btn .btn-green }

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

Download the [example data](https://zjueducn-my.sharepoint.com/:u:/g/personal/s_q_zju_edu_cn/EUrwsDgin4JKlxtsXY_qOcUBozki-kUY65-9BOvd2-AzbQ?e=OOVqCF). For convenient downloads, we just upload the compressed videos, you should first extract images from the videos:

```bash
data=<path/to/example/data>
# extract the images
python3 apps/preprocess/extract_image.py ${data}
```

Then you should extract the vertices from the SMPL parameters:

```bash
python3 apps/postprocess/write_vertices.py ${data}/output-smpl-3d/smpl ${data}/output-smpl-3d/vertices --cfg_model ${data}/output-smpl-3d/cfg_model.yml --mode vertices
```


### Install

First you should install the `easymocap` environment. This project depends on: `pytorch-lightning`, `spconv`. See `requirements_neuralbody.txt` for more details.

```bash
pip install -r requirements_neuralbody.txt
```

### Train

```bash
data=/path/to/dataset
# Recommand training with 4x3090
python3 apps/neuralbody/demo.py --mode soccer1_6 ${data} --gpus 0,1,2,3
# Reduce the number of rays if you train with RTX 1080Ti/3060
python3 apps/neuralbody/demo.py --mode soccer1_6 ${data} --gpus 0, data_share_args.sample_args.nrays 1024
```

### Demo

```bash
# render with 4x3090
python3 apps/neuralbody/demo.py --mode soccer1_6 ${data} --gpus 0,1,2,3 --demo
# (not recommand)
python3 apps/neuralbody/demo.py --mode soccer1_6 ${data} --gpus 0, data_share_args.sample_args.nrays 1024 --demo
```

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
@inproceedings{shuai2022multinb,
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
