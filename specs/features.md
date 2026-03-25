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

## 3. Aspect Ratio (Global)

- A single global aspect ratio selector shared across all models
- Preset options: **1:1, 16:9, 4:3, 3:2, 9:16, 2:3**
- Each model plugin maps the chosen ratio to its own optimal pixel dimensions (e.g. 1:1 → 1024×1024 for SDXL-based models, 768×768 for others)
- Width/height are not exposed as raw inputs — the aspect ratio is the only dimension control

## 4. Model Settings

- Each model exposes its own set of configurable parameters (excluding dimensions, which are global)
- Settings are grouped per model and collapsible
- Each setting displays:
  - Name
  - Current value (editable input)
  - Human-readable explanation of what the setting does
  - Valid range or options
  - A **"Random"** toggle button (see below)

### Seed

- Each model has a **seed field** — auto-populated with a random value on page load and before each new generation
- The seed field is always editable — the user can type in a specific seed to reproduce a result
- A 🎲 button next to the field re-randomises the seed manually
- The seed used is always saved to the database with the generation record

## 5. Random Mode (Per Setting)

When a setting has "Random" enabled:
- Instead of using the specified value, the system generates **5 images** with that setting varied across its valid range
- All other settings remain fixed
- The resulting images are displayed in a grid with the varied setting value labeled under each image
- This allows visual exploration of how that specific parameter affects output
- The number of variants is fixed at **5** (not user-configurable)
- **Only one setting can have Random enabled at a time** — enabling Random on a setting automatically disables it on any previously selected setting (radio-style behaviour)
- The 5 values are **evenly spaced** across the setting's valid range (e.g., for Steps 1–100: values would be 10, 28, 46, 64, 82)

## 6. Image Generation

- User clicks "Generate"
- Images are generated for each selected model (sequentially due to VRAM constraints)
- Progress is shown per model (e.g., spinner, step counter if available)
- Results appear as they complete — no need to wait for all models

## 7. Comparison View

- All generated images from a single run are displayed side by side
- Each image is labeled with: model name, key settings used
- Images can be clicked to view full resolution
- Option to download individual images

## 8. Generation History & Persistence

- Every generation is saved to SQLite with full metadata:
  - Prompt (positive and negative)
  - Model used
  - All settings at time of generation
  - Timestamp
  - Output image path/file reference
- Storage is automatic and requires no user action

## 9. Gallery

See [gallery.md](gallery.md).
