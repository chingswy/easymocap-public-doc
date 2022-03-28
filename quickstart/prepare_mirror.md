---
layout: default
title: Prepare Your Mirrored-Human Dataset
parent: Quick Start
nav_order: 3
---

# Prepare Your Mirrored-Human Dataset
{: .no_toc }

1. TOC
{:toc}
---

## Download the videos from Youtube

Find some channels in the YouTube like [ 잇츠유림 It's U Limn ](https://www.youtube.com/channel/UChRjZQ9i7Ci1pfYsEC_syMg). In their homepage, you may find many related videos like [this](https://www.youtube.com/watch?v=homrg6ZZMRY).

Given the youtube link, we will try to download its max resolution:

```bash
# install the pytube
python3 -m pip install pytube
# download the video given the url
database=data/youtube
python3 scripts/dataset/download_youtube.py "https://www.youtube.com/watch?v=homrg6ZZMRY" --database ${database}
```

## Extract the images and mannually clip

First extract the images.

```bash
# extract the videos to images
python3 apps/preprocess/extract_image.py ${database}
```

Mannually clip the images:

```bash
python3 apps/annotation/annot_clip.py ${database}
```

Main operations: `a/d` for previous/next frame, `w/s` for previous/next 100th frame. `j` for recoding the start of the clip; `k` for recording the end of the clip; `l` for add this clip to database. 

|The arrow at the top indicates the current loaction|After press `j`, the red arrow show the start position|After press `k`, the right red arrow show the end position|
|----|----|----|
|![](../images/annot_clip_0.jpg)|![](../images/annot_clip_j.jpg)|![](../images/annot_clip_k.jpg)|
|After press `l`, the clips will be red.|Repeat this operation, you can record multiple clips.|
|![](../images/annot_clip_l.jpg)|![](../images/annot_clip_two.jpg)||


After this annotation, copy the clips to `${data}`

```bash
data=/path/to/output
python3 apps/annotation/annot_clip.py ${database} --copy --out ${data}
```

## Detect and track the human

```bash
python3 apps/preprocess/extract_keypoints.py ${data} --mode yolo-hrnet
```

