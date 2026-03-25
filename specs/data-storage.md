# Data Storage

## Database

- **Engine:** SQLite (via Bun's native SQLite API)
- **Location:** Local file, e.g., `./data/images.db`
- **Purpose:** Store all generation metadata and link to output images

## Image Files

- Generated images saved to local disk (e.g., `./output/<timestamp>-<model>-<seed>.png`)
- Database stores the file path reference
- Images are never deleted automatically

## Schema (Draft)

### `generations` table

| Column | Type | Description |
|--------|------|-------------|
| id | INTEGER PK | Auto-increment |
| created_at | DATETIME | Timestamp of generation |
| prompt | TEXT | Positive prompt |
| negative_prompt | TEXT | Negative prompt (nullable) |
| model_id | TEXT | Model plugin identifier |
| settings | JSON | Full settings object used |
| image_path | TEXT | Relative path to output image file |
| generation_time_ms | INTEGER | How long the generation took |
| run_id | TEXT | Groups images from the same "Generate" button click |

### `runs` table

| Column | Type | Description |
|--------|------|-------------|
| id | TEXT PK | UUID for the generation run |
| created_at | DATETIME | Timestamp |
| prompt | TEXT | Prompt used for this run |
| negative_prompt | TEXT | Negative prompt (nullable) |
| models_used | JSON | List of model IDs used in this run |

## Notes

- `run_id` links all images generated from a single click of "Generate"
- `settings` stored as JSON to be flexible across different model plugins
- Schema should support querying by model, prompt, date range, and run
