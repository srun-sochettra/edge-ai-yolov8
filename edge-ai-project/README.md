# Edge AI lab workspace

This directory contains the executable YOLOv8 exercises. Start with the [repository overview](../README.md) for the lab map, limitations and responsible-use guidance.

## Working-directory quick start

From this directory, using Windows PowerShell:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Create `models/` and place a trusted `yolov8n.pt` there. Weights are not included in the export. Then run:

```powershell
python src/gpu_test.py
python src/test_opencv.py
python src/test_yolo.py
python src/lab_6_2_webcam_detection.py
```

Camera scripts request DirectShow and use OpenCV desktop windows. A headless environment or different capture backend requires separate adaptation. Lowercase `q` exits camera loops.

The ONNX export script creates `models/yolov8n.onnx`; the following metadata script does not run inference. See the root README before interpreting benchmark results.

Runtime logs and snapshots belong in `logs/` and `outputs/`, which the existing ignore rules exclude. Ignoring a path does not remove previously tracked files or make sensitive recordings safe to share.

No runtime checks were performed during this documentation refresh.
