---
name: genai-model-router
description: >-
  Proactive generative AI model router and upstream git synchronizer. Automatically evaluates incoming
  user prompts across Text, Image, Video, Avatar, and Audio modalities and routes execution to Hedra v3,
  Happy Horse 1.0, Llama 4, Qwen 3.5, FLUX.1/2, LTX-2.5, Wan 2.2, Tencent MusePose, Whisper Large V3, or Bark.
---

# Proactive Generative AI Model Router & Upstream Sync

This skill governs the automatic selection, invocation, and upstream git synchronization of open-source and API-backed generative models in the workspace.

## Behavioral Triggers

Activate this skill automatically whenever a user prompt involves:
- **Avatar & Talking Head Video**: Routes to **Hedra v3 Unified API** (`https://api.hedra.com/v3`).
- **Joint Audio-Video & Fast 1080p Generation**: Routes to **Happy Horse 1.0** (`15B Transformer`) or **LTX-2.5**.
- **Long Single-Shot Cinematic Video**: Routes to **Wan 2.2 / Wan 3.0**.
- **Human Dance & Pose Animation**: Routes to **Tencent MusePose** (`musepose-generate`).
- **High-Resolution Image & Typography**: Routes to **FLUX.1 [schnell] / FLUX.2**.
- **Speech-to-Text & Subtitle Alignment**: Routes to **Whisper Large V3**.
- **Voice Synthesis & Sound Effects**: Routes to **Bark / XTTS**.
- **Multimodal Vision & Long-Context Reasoning**: Routes to **Qwen3.5-VL**, **Llama 4**, or active **LM Studio** local endpoints.

## Global CLI Commands

1. **Proactive Prompt Routing**: `genai-route "<user prompt>"`
2. **List Configured Master Catalog**: `genai-route --list-catalog`
3. **Upstream Git Synchronization**: `genai-sync` (or `genai-sync --clone`)
4. **Post-Render Playback Handoff**: `render-play <output.mp4>`