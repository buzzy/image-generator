# Supported AI Models

## Architecture

The backend uses a **plugin-based model architecture**. Each model is an independent module that implements a shared interface, allowing:
- New models to be added by creating a new plugin file
- Each model to define its own unique settings and parameters
- The frontend to dynamically render model-specific settings based on the plugin's schema

## Initial Models

### 1. FLUX.2 — Black Forest Labs
- **Variant:** Best model variant that fits within 24GB VRAM (likely FLUX.1-dev or FLUX.1-schnell quantized)
- **Known settings:** Steps, CFG scale, seed, sampler, width, height, guidance

### 2. Stable Diffusion 3.5 — Stability AI
- **Variant:** SD 3.5 Large or SD 3.5 Large Turbo (depending on VRAM fit at 24GB)
- **Known settings:** Steps, CFG scale, seed, sampler, negative prompt, width, height

### 3. Qwen-Image — Alibaba
- **Variant:** Best variant that fits within 24GB VRAM
- **Known settings:** TBD — to be defined during model integration

### 4. Illustrious / Noob — Stable Diffusion Derivatives
- **Variant:** Illustrious XL or NoobAI XL (SDXL-based derivatives)
- **Known settings:** Steps, CFG scale, seed, sampler, negative prompt, width, height, LoRA support (optional)

## Plugin Interface

Each model plugin must expose:
- **Metadata:** Name, description, homepage/source link
- **Settings schema:** List of all configurable parameters with name, type, default value, valid range/options, and human-readable explanation
- **Generate function:** Accepts prompt + settings, returns image(s)
- **Health check:** Reports whether the model is loaded and ready

## VRAM Management

- Models are loaded on-demand to avoid exceeding 24GB VRAM
- Only one model should be loaded at a time unless VRAM allows multiple
- Loading state should be surfaced in the UI
