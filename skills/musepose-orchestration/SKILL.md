---
name: musepose-orchestration
description: >-
  Autonomous orchestration of Tencent MusePose image-to-video human dance animation and ComfyUI/Python backends.
  Audits local asset directories, matches single-person portrait frames with skeleton sequences, handles CUDA OOM recovery,
  and automatically routes rendered videos to render-play.
---

# Tencent MusePose Autonomous Agent Doctrine

This skill governs Antigravity agents executing human dance and pose animation workflows via Tencent MusePose, ComfyUI, or headless Python scripts.

## Behavioral Triggers & Intent Routing

Activate this skill when:
- The user requests to animate a portrait photo with a dance video or motion skeleton.
- Running headless MusePose pipelines (`pose_align.py`, `test_stage_2.py`, or ComfyUI API nodes).
- Verifying asset readiness (portraits, driving videos, DW-Pose/OpenPose keypoint sequences).
- Diagnosing CUDA OOM, PyTorch memory bottlenecks, or missing checkpoints.

## The 5-Phase Agent Workflow

1. **Phase 1: Asset Auditing**: Verify portrait is divisible by 64 (`512x512` or `768x768`) and driving video aspect ratio matches via `ffprobe`.
2. **Phase 2: Checkpoint Verification**: Verify weights in `pretrained_weights/` (`dw-ll_ucoco_384.pth`, `denoising_unet.pth`, `reference_unet.pth`, `pose_guider.pth`, `motion_module.pth`).
3. **Phase 3: Pose Alignment**: Run `python pose_align.py --img_path <img_path> --video_path <video_path> --out_dir ./output/aligned`.
4. **Phase 4: Headless Execution & Self-Healing**: Run `musepose-generate --config configs/test_stage_2.yaml`. On CUDA OOM, downscale `W`/`H` to `512`, set `C: 2`, and `S: 2`.
5. **Phase 5: Autonomous Playback**: Launch rendered output via `render-play ./output/generated_dance.mp4 --intent animation`.