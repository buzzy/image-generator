# Project Overview

## What It Is

A local web application for generating images using multiple AI models simultaneously. The primary purpose is to allow direct comparison of outputs across different AI image generation engines using the same prompt and settings.

## Target User

Single local user (the developer/owner). No authentication required. Runs entirely on local hardware.

## Hardware Target

- GPU: NVIDIA RTX 3090 (24GB VRAM)
- All models must be selected and configured to work within this hardware constraint.

## Goals

1. **Multi-model comparison** — Generate the same prompt across multiple models in one action and view results side by side.
2. **Pluggable model architecture** — New models can be added without major refactoring. Each model is an independent backend plugin.
3. **Per-setting exploration** — A "random" mode for any individual setting generates multiple images varying only that setting, enabling visual exploration of its effect.
4. **Persistent history** — Every generation is stored with full metadata in a local SQLite database.
5. **Gallery browsing** — Browse and filter all previously generated images.

## Stack

- **Backend:** Bun (pure, no Node.js)
- **Frontend:** Vue
- **Database:** SQLite (via Bun's native SQLite support)
- **Scope:** Local only — no deployment, no authentication, no cloud services
