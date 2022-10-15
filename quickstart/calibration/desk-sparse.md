---
layout: default
title: DeskStage
parent: Calibration
grand_parent: Quick Start
nav_order: 300
nav_exclude: true
published: false
---

# DeskStage相机标定

## 0. 连接手机

**IDR**:
- 检查手机的wifi连接，需要连接到IDR-EAP-5G
- 打开DroidCam软件，上面会显示一个10.0.网段的地址。

**Windows**平台：
- 在主机上打开Xlaunch，确保选中第三个选项`Disable access control`。
- 进入WSL，切换到`easymocap`代码目录
- `export DISPLAY=<ip>:0.0`

**Linux**平台：
- 无特殊操作

对于每个相机，例如ip是`10.0.233.126`，单独检查这个相机是否可以正常显示：
```bash
python3 apps/camera/detect_server_one.py "http://10.0.233.126:4747/video/v3/avc/1280x720" --show --back --noblock
```

修改`config/camera/usb-logitech-windows.yml` 文件。从上至下，依次吧相机id改为中间，左边，右边的手机的地址。配置完成后，检查相机是否可以正常显示，并且调整位置和视野。

```bash
python3 apps/camera/realtime_display.py --cfg config/camera/usb-logitech-windows.yml --display --num 100000
```

检查相机是否可以正常读取，如果一切正常，那么没问题；

- 如果有的视角比较卡顿，检查一下网络连接，或者重启
- 如果相机不能访问，尝试ping一下相机，或者重启相机
- 如果相机可以访问，但是不能显示，检查一下Xlaunch是否正常打开，检查`xeyes`（通过`sudo apt install x11-utils`安装）是否可以正常显示

相机视角调整方式：

```bash
python3 apps/camera/realtime_display.py --cfg_cam config/camera/usb-logitech-windows.yml --display
```

1. 放置主视角的相机
2. 在主视角上确定人的位置，确保人在的活动区域可以看到人的上半身。
3. 固定住人的位置，调整侧面两个相机的位置和朝向，需要让人处于侧面两个相机的中央。

**以下代码需要设置`root=data/deskstage/<date>`，其中`<date>`表示当天的日期，例如0706**

## 1. 相机内参标定

缓慢晃动棋盘格，不断用不同角度倾斜棋盘格。

```bash
python3 apps/camera/realtime_display.py --cfg_cam config/camera/usb-logitech-windows.yml --display --num 1000 --out ${root}/ba
```

## 2. 相机外参标定

将棋盘格平行于身体平面，横着拿，左手拿到黑色角落的一边。保持静止

```bash
python3 apps/camera/realtime_display.py --cfg config/camera/usb-logitech-windows.yml --display --num 100 --out ${root}/ground
```

一键化标定脚本：
```
./apps/calibration/calib_scripts_example.sh ${root}
```

## 3. 运行

**Windows:**

在WSL外面开启可视化窗口

```bash
cd D:\Work\easymocappublic\ && python apps/vis/vis_server.py --cfg config/vis3d/o3d_scene_half.yml --opts host 0.0.0.0 port 9999 block False
```

在WSL里面开启程序

```bash
python3 scripts/desktopstage/call.py ik-windows ${root} --vis3d 172.24.0.1:9999
```

**Linux:**

开启可视化：

```bash
python3 apps/vis/vis_server.py --cfg config/vis3d/o3d_scene_half.yml --opts host 0.0.0.0 port 9999 block False
```

开启关键点检测：

```bash
python3 apps/camera/detect_server.py --cfg_cam config/camera/usb-logitech-windows.yml --host 0.0.0.0:8888 --cfg_det config/camera/mediapipe-holistic.yml --timer
```

开启代码：

```bash
python3 apps/fit/triangulate1p.py --cfg_data config/recon/socket_mv1p.yml --opt_data args.camera ${root}/ground1f --cfg_exp config/recon/ik_halfbody.yml --vis3d localhost:9999 --det2d 0.0.0.0:8888 --no_write
```

