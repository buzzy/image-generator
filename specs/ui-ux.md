# UI & UX

## Layout

Two main sections accessible via top navigation:

1. **Generator** — The main image generation interface
2. **Gallery** — Browse all previously generated images

## Generator Page Layout

```
[Top Nav: Generator | Gallery]

[Prompt Input — large textarea]
[Negative Prompt — single global field, collapsible]

[Aspect Ratio Selector — global]
  ○ 1:1  ○ 16:9  ○ 4:3  ○ 3:2  ○ 9:16  ○ 2:3

[Model Selection Bar]
  ☑ FLUX.2   ☑ Stable Diffusion 3.5   ☑ Qwen-Image   ☑ Illustrious/Noob

[Settings Panel — per model, collapsible]
  ▼ FLUX.2 Settings
    Steps: [20] [?] [🎲 Random]
    CFG Scale: [7.5] [?] [🎲 Random]
    ...
  ▼ Stable Diffusion 3.5 Settings
    ...

[Generate Button]

[Results Area — side-by-side image grid]
  [FLUX.2 result]  [SD 3.5 result]  [Qwen result]  [Illustrious result]
```

## Settings Panel

- Each setting row: label | input | info icon (hover = explanation) | random toggle
- When "Random" is toggled on for a setting, the input is replaced with a range/count indicator
- Settings collapse per model to reduce clutter

## Results Display

- Images appear as they are generated (streaming results, not waiting for all)
- Each image card shows: model name, generation time, key settings summary
- Click image → full resolution lightbox
- Download button per image

## Feedback & State

- Model loading indicator (shown when a model is being loaded into VRAM)
- Per-model progress during generation (step X of Y if available, else spinner)
- Error state per model (shows error message inline without blocking other models)

## Responsive Design

- Designed for desktop use (local tool)
- Minimum supported width: 1280px
