---
name: media-player-router
description: >-
  Universal cross-platform media player launcher, video inspector, and audio/video preview router.
  Handles robust playback execution across Windows, macOS, and Linux by scoring open-source players
  (mpv, MPC-HC, MPC-BE, SMPlayer, VLC), providing detached non-blocking playback, automated ffprobe inspection,
  and seamless fallback via the global render-play CLI.
---

# Media Player Router & Playback Verification Skill

This skill guides the safe, reliable, and intelligent routing of rendered video and audio deliverables to the optimal open-source desktop player using `render-play` / `media-router`.

---

## 🧭 When to Use This Skill

Activate this skill whenever:
- A video or audio rendering process completes (HyperFrames, Remotion, FFmpeg, n8n, etc.).
- Launching an OS media player to preview rendered media assets without blocking the terminal.
- Routing playback according to intent (`--intent animation`, `prores`, `dark-ui`, `gui`, `inspect`).
- Verifying video metadata (duration, resolution, framerate, codec, bitrate) before user presentation.
- Overcoming Windows COM server execution errors (`WinError -2146959355`).

---

## ⚡ The Scoring & Decision Matrix

The router inspects video attributes with `ffprobe` and computes fit scores across 5 premier open-source players:

| Player | Winget Identifier | Ideal Use Case | Special Capabilities |
| :--- | :--- | :--- | :--- |
| **mpv** | `shinchiro.mpv` | Short animations (<45s), kinetic typography, micro-videos | Minimalist UI, instantaneous launch, auto-looping (`--loop`), frame stepping (`,` / `.`) |
| **MPC-HC (clsid2)** | `clsid2.mpc-hc` | ProRes, DNxHD, 4K/8K mastering, high-bitrate scrubbing | DirectShow hardware acceleration, zero-lag scrubbing on >25 Mbps files |
| **MPC-BE** | `MPC-BE.MPC-BE` | Visual client presentations, dark aesthetic review | Sleek dark UI, seekbar hover thumbnail preview generation |
| **SMPlayer** | `RicardoVillalba.SMPlayer` | In-depth speech analysis, variable speed review | Dedicated GUI speed sliders, A-B repeat, customizable audio filters |
| **VLC** | `VideoLAN.VLC` | Universal fallback, format resilience, diagnostics | Maximum codec tolerance, stream information / dropped frames analysis (`Ctrl+J`) |

---

## 🚀 Global CLI Commands

The router is installed globally at `~/.local/bin` and can be invoked from any shell or python script:

```bash
# 1. Standard auto-routing
render-play "output.mp4"

# 2. Short animation or kinetic typography
render-play "animation.mp4" --intent animation

# 3. ProRes / High-Bitrate Master
render-play "master.mov" --intent prores

# 4. Stream inspection & audio sync diagnostics
render-play "deliverable.mp4" --intent inspect

# 5. Scan host system for installed players
render-play --scan-only

# 6. Dry run scoring without launching
render-play "output.mp4" --dry-run
```

---

## 🛡️ Non-Blocking Detached Execution

On Windows, the router spawns players with `subprocess.DETACHED_PROCESS | subprocess.CREATE_NEW_PROCESS_GROUP`, ensuring the terminal or agent execution loop returns immediately without freezing background pipelines.
