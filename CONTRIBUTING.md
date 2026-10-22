# Contributing

Keep changes focused on a particular lab and its learning objective. Read the [README](README.md) before changing model paths, capture behaviour or output formats.

## Development

Use the existing project requirements and a separate Python environment. Record actual Python, dependency, device and driver versions when reporting a problem. Minimum dependency ranges are not a tested lockfile.

Preserve script-relative model/output paths and existing controls unless a deliberate change is documented. Do not add a service framework, shared configuration abstraction or new inference backend without a concrete need.

## Verification

Distinguish syntax checks, import checks, model loading, actual inference, camera capture, ONNX export and device benchmarks. Report only what was executed. The scripts named test_opencv.py and test_yolo.py are manual smoke checks, not an automated assertion-based test suite.

For changed logic, add a small regression check where practical. Relevant cases include ROI boundary centres, the exact alert threshold, missing model files, failed camera reads, repeated crossings, tracker ID changes and output-write failures.

For benchmark changes, report input data, warm-up, iteration count, backend/device, timing boundary and resource-measurement method. Check output correctness before comparing speed. Do not infer accuracy from random-noise inference or end-to-end FPS from model-call timing.

Use permitted camera data and redact logs/screenshots before sharing. Describe the problem, focused change, verification, remaining gaps and any output-format compatibility impact in a pull request. Follow [SECURITY.md](SECURITY.md) for sensitive concerns.
