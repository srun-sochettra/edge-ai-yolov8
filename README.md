# Edge AI with YOLOv8

**From webcam detections to tracking, crossing events and a local monitoring dashboard.**

A Python lab collection exploring local computer-vision inference with YOLOv8 Nano, OpenCV and ONNX tooling. The exercises build from environment checks and webcam detection to region-based analytics, people-count alerts, object tracking and CSV logging.

This repository contains workshop exercises, not a deployed edge appliance or a production monitoring service. No device-specific performance or detection-accuracy results are claimed here.

## Lab map

All scripts are under [edge-ai-project/src](edge-ai-project/src/).

| Lab | Script | What the code does |
| --- | --- | --- |
| Environment | `gpu_test.py` | Reports PyTorch and CUDA availability |
| Camera | `test_opencv.py` | Opens the default webcam and attempts one frame read |
| Model | `test_yolo.py` | Loads local weights and runs inference on random noise |
| 6.2 | `lab_6_2_webcam_detection.py` | Displays annotated webcam detections |
| 6.3 | `lab_6_3_export_onnx.py` | Exports local weights to a fixed-shape ONNX model |
| 6.4 | `lab_6_4_onnx_inference.py` | Creates an ONNX Runtime session and prints provider/input/output metadata; does not execute a prediction |
| 6.5 | `lab_6_5_benchmark.py` | Compares model-call timing for PT and ONNX through the Ultralytics wrapper |
| 7.1 | `lab_7_1_roi_detection.py` | Filters detections by a drawn rectangle, logs counts and saves snapshots on request |
| 7.3 | `lab_7_3_people_counter_alert.py` | Counts person detections and displays an alert above the configured threshold |
| 8.1 | `lab_8_1_multi_object_tracking.py` | Displays persistent tracking IDs and movement trails |
| 8.2 | `lab_8_2_line_crossing_counter.py` | Logs directional crossings of a horizontal line using tracked centres |
| 9.1 | `lab_9_1_monitoring_dashboard.py` | Combines video, detection summaries and resource metrics in an OpenCV window |

The dashboard is a desktop window, not a browser application. Tracking IDs are session-level tracker labels, not verified identities.

## Local setup

### Requirements

- Python with a compatible installation of the packages in [requirements.txt](edge-ai-project/requirements.txt). No Python version or dependency lockfile is pinned in the supplied export.
- A graphical desktop and webcam for camera labs.
- A trusted local `yolov8n.pt` model file. Model binaries are excluded from the supplied export and ignored by the project rules.

Camera scripts explicitly request `cv2.CAP_DSHOW`. Treat the current capture path as Windows-oriented; other platforms need an appropriate backend change and testing. CUDA acceleration is not guaranteed by installing the requirements file.

### Install

Run from the repository root. The following activation command is for Windows PowerShell:

```powershell
cd edge-ai-project
python -m venv venv
.\venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
```

Use the activation method appropriate to your shell if different. The requirements specify minimum versions, not a reproducible tested environment.

Create a `models` directory inside `edge-ai-project` and place the trusted model at:

```text
edge-ai-project/models/yolov8n.pt
```

The scripts check that path before loading. They do not implement a model-download command. Review the model's source and applicable terms before using or redistributing it.

### Start with the checks

From inside `edge-ai-project`:

```powershell
python src/gpu_test.py
python src/test_opencv.py
python src/test_yolo.py
python src/lab_6_2_webcam_detection.py
```

The random-noise check establishes only that a model call can execute in your environment. Its success message is not evidence of detection accuracy or complete system health.

### Export and compare

```powershell
python src/lab_6_3_export_onnx.py
python src/lab_6_4_onnx_inference.py
python src/lab_6_5_benchmark.py
```

Export requests `imgsz=640`, `opset=17`, `simplify=True` and `dynamic=False`. The requirements do not explicitly list every export/simplification dependency; resolve any additional requirements against the actual installed tool versions. No successful export is claimed by this documentation.

The benchmark needs both `models/yolov8n.pt` and `models/yolov8n.onnx`. It writes `outputs/benchmark_results.csv` and `outputs/benchmark_chart.png`.

### Explore the analytics

```powershell
python src/lab_7_1_roi_detection.py
python src/lab_7_3_people_counter_alert.py
python src/lab_8_1_multi_object_tracking.py
python src/lab_8_2_line_crossing_counter.py
python src/lab_9_1_monitoring_dashboard.py
```

Run one camera lab at a time. Edit the constants in the relevant script for camera index, confidence and other options; there is no shared command-line configuration layer.

## Controls and outputs

- Camera loops support lowercase `q` to quit.
- ROI lab: drag with the left mouse button to set a rectangle; `r` resets it, `s` saves the annotated display, and `+`/`-` adjust confidence. The ROI lab also accepts uppercase letter variants.
- Line-crossing lab: lowercase `r` resets counters and tracking-side state.
- CSV logs are written under `edge-ai-project/logs/`; ROI snapshots are written under `edge-ai-project/outputs/snapshots/`.

ROI inclusion uses a detection box's centre, not full-box containment. The people alert activates when the count is **greater than 3** by default, not when it equals 3. Counts and crossing events are model-derived estimates, not audited occupancy measurements.

## Interpreting performance

The benchmark uses one random 640 × 640 image, ten warm-up calls and 100 measured calls per model. It reports mean/P95 call latency, loop throughput, sampled CPU usage and process resident memory.

These measurements are not camera-to-display latency, accuracy evaluation or a hardware-neutral speed comparison. Backend/device selection is not fixed explicitly in the benchmark. Its CPU figure averages samples before and after the loop rather than measuring the full workload. Process memory can include state retained from the preceding model run. No benchmark results are included in this refresh.

## Repository layout

```text
README.md                         Project overview
Edge AI Inference Workshop.html   Supplied workshop material
edge-ai-project/
  README.md                       Working-directory quick start
  requirements.txt                Minimum dependency versions
  src/                            Standalone lab scripts
  models/                         Local model files, not supplied
  logs/                           Runtime CSV output
  outputs/                        Benchmark files and snapshots
```

The runtime directories shown above are expected paths, not bundled model files or recorded results.

## Responsible use

Use cameras only with appropriate permission. Snapshot files can contain recognisable people and surroundings; timestamped logs can reveal activity patterns. Keep them out of public commits and choose an appropriate retention period. See [SECURITY.md](SECURITY.md) for data-handling guidance and [CONTRIBUTING.md](CONTRIBUTING.md) for verification expectations.

## Verification and licence

This refresh inspected the Python source and parsed its syntax. It did not install dependencies, load models, access a camera, export ONNX, run benchmarks or test a GPU/edge device.

No project licence file is included in the supplied export. This refresh does not assign a licence or establish rights to the workshop material, model weights or third-party dependencies. Confirm those separately before redistribution.
