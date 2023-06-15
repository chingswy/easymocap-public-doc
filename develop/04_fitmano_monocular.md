
## Run the code

The example dataset can be download from [313_rawvideos+annots.zip](http://gofile.me/66p77/5bnFUgpmq). After downloading, unzip it to the `data/examples` folder.

```bash
data=data/examples/313
emc --data config/datasets/mv1p.yml --exp config/mv1p/triangulate_and_fitSMPL.yml --opt_data args.root ${data}
```

The results can be found in `output/fitmanofix`.


- `dataset`:读取单帧2D关键点、对应的图片
- `at_step`:
    - 使用网络估计HandMesh
    - 估计在全图里的RT
- `at_final`: 完成了每一帧的估计之后，我们将组合所有帧的初始化SMPL估计结果、所有帧的2D关键点，一起联合优化。


