# Core Features

## 1. Prompt Input

- Large text area for the main (positive) prompt
- **One global negative prompt field** shared across all selected models — models that don't support negative prompts (e.g. FLUX.2) simply ignore it
- Both prompts are shared across all selected models in a generation run

## 2. Model Selection

- Checkboxes for each available model
- All models checked by default
- User can deselect models to exclude them from the current generation
- Each model shows its current status (loading, ready, unavailable)

## 3. Model Settings

- Each model exposes its own set of configurable parameters
- Settings are grouped per model and collapsible
- Each setting displays:
  - Name
  - Current value (editable input)
  - Human-readable explanation of what the setting does
  - Valid range or options
  - A **"Random"** toggle button (see below)

## 4. Random Mode (Per Setting)

When a setting has "Random" enabled:
- Instead of using the specified value, the system generates **5 images** with that setting varied across its valid range
- All other settings remain fixed
- The resulting images are displayed in a grid with the varied setting value labeled under each image
- This allows visual exploration of how that specific parameter affects output
- The number of variants is fixed at **5** (not user-configurable)
- **Only one setting can have Random enabled at a time** — enabling Random on a setting automatically disables it on any previously selected setting (radio-style behaviour)
- The 5 values are **evenly spaced** across the setting's valid range (e.g., for Steps 1–100: values would be 10, 28, 46, 64, 82)

## 5. Image Generation

- User clicks "Generate"
- Images are generated for each selected model (sequentially due to VRAM constraints)
- Progress is shown per model (e.g., spinner, step counter if available)
- Results appear as they complete — no need to wait for all models

## 6. Comparison View

- All generated images from a single run are displayed side by side
- Each image is labeled with: model name, key settings used
- Images can be clicked to view full resolution
- Option to download individual images

## 7. Generation History & Persistence

- Every generation is saved to SQLite with full metadata:
  - Prompt (positive and negative)
  - Model used
  - All settings at time of generation
  - Timestamp
  - Output image path/file reference
- Storage is automatic and requires no user action

## 8. Gallery

See [gallery.md](gallery.md).
