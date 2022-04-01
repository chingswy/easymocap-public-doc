## Set your camera


## Test video capture

```bash
python3 apps/camera/realtime_display.py --cfg_cam config/camera/folder.yml --opt_cam args.root ${data}
python3 apps/camera/realtime_display.py --cfg_cam config/camera/usb-logitech.yml --display
```

## Calibrate camera

```bash
python3 apps/calibration/detect_chessboard.py ${data} --out ${data}/output --pattern 11,8 --seq --grid 0.03 --max_step 40 --min_step 10
python3 apps/calibration/calib_intri.py ${data} --num 200 --share_intri
python3 apps/calibration/calib_ba_by_chessbaord.py ${data} --intri ${data}/../031501/output/intri.yml --out ${data}/calib-share --share_intri
```

## Test realtime detector

```bash
python3 apps/camera/detect_server.py --cfg_cam config/camera/selfie.yml --cfg_det config/camera/mediapipe-selfie.yml
python3 apps/camera/detect_server.py --cfg_cam config/camera/folder.yml --cfg_det config/camera/mediapipe-holistic.yml --opt_cam args.root ${data}
```

## Run the code


## Performance

- 30ms for 3 cameras capture
- 120 ms for detection

## TODO

- [x] multi-thread and queue for camera capture
- [x] multi-thread for mediapipe
- [ ] calibration for dynamic cameras
- [ ] add faster GPU-based detector and estimator