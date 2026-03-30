# Core Features

## 1. Prompt Input

- Large text area for the main (positive) prompt
- **One global negative prompt field** shared across all selected models — models that don't support negative prompts (e.g. FLUX.2) simply ignore it
- Both prompts are shared across all selected models in a generation run
- No prompt presets or history — prompts are entered fresh each time or recovered via the Gallery's Reproduce button

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

Settings use a **shared-with-override** model:

- Settings that exist across multiple models (e.g. steps, CFG scale) have a **shared global value** shown in a "Shared Settings" panel above the per-model panels
- Each model's collapsible panel shows its own settings; shared settings appear with the current global value but can be **overridden per model**
- When a model is using an override, a visual indicator (e.g. a small dot or "custom" badge) marks that setting as overridden
- An override can be cleared to revert to the global shared value
- Settings unique to a specific model (not shared) appear only in that model's panel
- Changing a shared setting updates all models that are not individually overriding it

Each setting displays:
  - Name
  - Current value (editable input — shared or overridden)
  - Human-readable explanation of what the setting does
  - Valid range or options
  - A **"Random"** toggle button (see Random Mode section)
  - Override indicator where applicable

### Seed

- Each model has its own **seed field** (seeds are not shared, since identical seeds across different architectures produce different images anyway)
- Auto-populated with a random value before each generation
- Always editable — the user can type in a specific seed
- A 🎲 button re-randomises the seed
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
- **Generation queue** — if a generation is already running when the user clicks Generate, the new request is queued and starts automatically when the current one finishes
- Queue depth is unlimited; a queue indicator shows how many runs are pending
- Individual queued items can be cancelled before they start

### Error Handling

- If a model fails mid-generation (VRAM overflow, crash, timeout), its card shows an error message in place of the image
- Other models in the same run are unaffected and continue generating
- The failed card displays a **"Retry"** button — clicking it re-triggers just that model without starting a full new run
- Failed generations are saved to the database with an error status
- If the retry also fails, the error card updates with the new error message and the Retry button remains available

## 7. Comparison View & Results List

- The Generator page maintains a running list of all results from the current session — new runs are added to the top, older runs remain visible below
- As soon as a generation run starts, placeholder cards are immediately inserted at the top of the results list — one per model — in a **loading state**: blurred fake image with a spinner/loader overlay
- Once a model finishes, its placeholder is replaced by the real image in place (no layout shift)
- Each image card shows: model name, key settings summary, generation time (once complete)
- Images can be clicked to view full resolution
- Download button per image
- The session list is not persisted — refreshing the page clears it (full history is always in the Gallery)

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
