---
layout: default
title: Prepare Your Mirrored-Human Dataset
parent: Quick Start
nav_order: 5
---

# Prepare Your Mirrored-Human Dataset
{: .no_toc }

1. TOC
{:toc}
---

## Capture

Record the video by yourself or [download from YouTube](./capture_youtube.md)

```bash
database=data/mirror-youtube
python3 scripts/dataset/download_youtube.py "https://www.youtube.com/watch?v=hVDPS-f6K5o" --database ${database}
python3 apps/preprocess/extract_image.py ${database}
python3 apps/annotation/annot_clip.py ${database}
python3 apps/annotation/annot_clip.py ${database} --copy --out data/mirror-youtube-clip
```

## Extract keypoints

See [prepare keypoints](./keypoints.md#extract-keypoints) for detailed instruction.

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
# use OpenPose to detect the feet, skip it if you don't install OpenPose
python3 apps/preprocess/extract_keypoints.py ${data} --mode feetcrop --hand
# track the human
python3 apps/preprocess/extract_track.py ${data}
```

**case 1:** tracking failed because wrong clip, you should re-clip this sequence:

```bash
python3 scripts/preprocess/reclip.py ${data} --start 0 --end <right_end_frame> --delete
```

This script will auto create a new folder and copy the images and annotations to the new folder. `--delete` flag will help you to delete the original folder.

**case 2:** tracking failed because wrong bboxes, you should annotate the wrong bboxes:

```bash
python3 apps/annotation/annot_track.py ${data} --sub <the wrong sub>
# estimate the 2D keypoints
python3 apps/preprocess/extract_keypoints.py ${data} --mode hrnet --subs <the wrong subs> --force

```


<!-- ## One step reconstruction

```bash
xxx
```

The rendered results will be saved at `${data}/output-mirror/smplmesh/`.

If some bug occurs, you should run this algorithm step-by-step and check the results of each step.

## Detect and track the human

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
python3 apps/preprocess/extract_track.py ${data}
```

## Fitting SMPL

```bash
python3 apps/demo/mocap.py ${data} --mode mirror --mono
``` -->
