---
layout: default
title: Prepare for novel view 
parent: Install
nav_order: 4
---

# Novel View Synthesis

## Instant-ngp

```bash
mkdir -p 3rdparty && cd 3rdparty
git clone --recursive https://github.com/nvlabs/instant-ngp
cd instant-ngp
cmake . -B build
cmake --build build --config RelWithDebInfo -j 16
```