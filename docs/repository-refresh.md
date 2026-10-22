# Repository refresh

## Identity

Keep the repository slug **edge-ai-yolov8**. It already communicates the subject and model family. Use **Edge AI with YOLOv8** as the display title, with a clear lab-collection description rather than implying a deployed edge product.

Suggested GitHub description:

> Python computer-vision labs with YOLOv8: webcam detection, ONNX export, ROI analytics, tracking, line-crossing counts and a local dashboard.

Suggested topics: `python`, `yolov8`, `opencv`, `onnx`, `computer-vision`, `object-tracking`, `edge-ai`.

No GitHub settings, remote names, topics, commits or pushes were changed.

## Apply the overlay

Extract into the existing repository root. Add the root README, contributing/security guides and this document; replace the previously empty edge-ai-project/README.md. Preserve all Python source, requirements, ignore rules, workshop material and Git history. This is not a complete repository replacement.

## Editorial decisions

The root README now provides a source-backed lab map, Windows-oriented setup, expected model paths, controls, output locations and measurement limitations. The nested README provides a short working-directory entry point instead of duplicating the full guide.

The ONNX metadata script is not advertised as an executed prediction. The people alert's strict greater-than threshold is explicit. Tracking IDs and frame-level detections are not presented as unique identities or verified occupancy. No speedup, accuracy result, device deployment, screenshot or model download route was invented.

No licence, dependency pins, CI workflow, model files or code fixes were added. Workshop HTML was retained unchanged; its embedded material was not used as proof that a particular deployment succeeded.

## Implementation notes for later work

- Camera capture explicitly requests DirectShow. Portability needs a backend change and real target testing.
- ONNX export requests simplification, but export dependencies are not all explicitly declared in requirements.txt. Resolve against the installed tool versions rather than guessing pins.
- The ONNX metadata script creates a session without calling session.run.
- Benchmark model calls use the Ultralytics wrapper without an explicit fixed backend/device comparison. CPU sampling and retained process memory limit interpretation.
- Camera-lab FPS measures the timed model call, not the complete capture/display loop.
- Line crossing compares tracked box centres across a tolerance zone. Repeated crossings can create multiple events for the same ID; counts are not unique-person totals.
- Snapshot and log writes need runtime failure checks before claiming reliable persistence. The ROI snapshot path calls cv2.imwrite without checking its return value.

These are source observations, not executed failure reports or fixes.

## Verification boundary

All supplied Python files were read for documentation relevance and syntax-parsed without importing or executing them. Requirements, ignore rules and the empty nested README were inspected. The workshop HTML was inventoried, not exhaustively reviewed or rendered.

Documentation links, referenced script paths and archive bytes were checked. No dependency installation, camera/GPU access, model inference, ONNX export, benchmark or edge-device deployment was performed.

To revert, remove added documents and restore the original nested README using version control.
