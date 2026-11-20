# GCF Event Upload — Ecoscope Workflow

Ecoscope Desktop workflow that bulk-creates EarthRanger events of **any event
type** (v1 or v2) from a CSV. Desktop version of the TwigaTools **Event Upload**
page. The work is done by the `gcf_event_upload` task in
[ecoscope-workflows-ext-gcf](https://github.com/Giraffe-Conservation-Foundation/ecoscope-workflows-ext-gcf) (v0.2.1+).

## Loading into Ecoscope Desktop

1. **Workflow Templates → + Add Template**
2. Paste this repo's URL: `https://github.com/Giraffe-Conservation-Foundation/gcf-event-upload`

## How to use it — three runs

| Run | Action | You fill in | You get (results folder) |
|---|---|---|---|
| 1 | **Make template** | Data source, event type | `<event_type>_template.csv`, `<event_type>_field_guide.csv` |
| 2 | **Check file only** (default) | + full path to your filled CSV, time zone | `<event_type>_problems.csv` — nothing is sent to EarthRanger |
| 3 | **Check and import** | same as run 2 | events created; `<event_type>_import_results.csv` (CSV row → serial number) |

- **Event type:** its value (e.g. `giraffe_survey_encounter_nam`) or its name as shown in EarthRanger.
- **Field guide:** each column's type (free text, number, yes/no, date/time, dropdown, multi-select dropdown), whether it's required, and the allowed dropdown values.
- Only `event_datetime` is always required. Dropdowns accept the value or the label; multi-select values are separated by `;`. Slashed dates are read day first (20/11/2026).
- Every event's title is the event type's name; priority and state use EarthRanger's defaults.
- List fields (one entry per animal, e.g. herd lists) can't be filled from a flat CSV and are left empty.
- Max 2,000 rows per run. **Don't run Check and import twice on the same file** — the events would be duplicated.

## Files

| File | Purpose |
|------|---------|
| `spec.yaml` | Workflow definition |
| `pixi.toml`, `wt-compiler-env-overrides.toml` | Build environment |
| `.github/workflows/compile.yml` | Compiles on push to `main` and commits `ecoscope-workflows-gcf-event-upload-workflow/` |
| `layout.json` | Dashboard layout (one summary text widget) |
