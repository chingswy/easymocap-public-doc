
在这一部分中，你将学到如何基于动作捕捉的结果，实现人体三维重建与自由视点渲染。

我们的方法主要基于neuralbody，当然与其类似的方法aninerf也可以使用


## Try the code

预处理：

```bash
# convert the SMPL parameter to vertices
python3 apps/postprocess/write_vertices.py ${data}/output-smpl-3d/smpl ${data}/output-smpl-3d/vertices --cfg_model config/model/smpl.yml --mode vertices
# render the instance map
python3 apps/postprocess/render.py ${data} --exp output-smpl-3d --mode instance-d0.05 --ranges 0 200 1 --model config/model/smpl.yml
```

检查：

```bash
python3 apps/neuralbody/check_trainset.py --cfg config/neuralbody/dataset/multiview/lightstage.yml --opts split train data_share_args.root ${data}
```


