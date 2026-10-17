# BharatYatra — Interactive India Travel Map

A travel planner for India: 289+ curated places (and growing) across 8 categories and 34 states/UTs, with marker clustering, state-level lazy loading, Wikipedia photos, and a vintage-atlas map.

## Deploy in 5 minutes (GitHub Pages)

1. Create a new GitHub repository (e.g. `bharatyatra`)
2. Upload the entire folder structure:
   ```
   index.html
   india-boundary.geojson
   highlights.json
   states-index.json
   rj.json, kl.json, up.json, ... (34 state files, all in the repo root)
   ```
3. Go to **Settings → Pages → Source** → select `main` branch, `/ (root)` → Save
4. Live at `https://YOUR_USERNAME.github.io/bharatyatra/`

## How it works

- **Country view**: shows 153 highlight places, clustered into coloured groups so the map stays clean even with thousands of pins.
- **Zoom into a state**: the site auto-loads that state's full dataset (lazy). A dropdown also lets visitors pick a state directly.
- **Category pills + State dropdown**: work together as filters. Both update the sidebar list and map markers.
- **On phones**: the controls collapse into one compact row — a **Categories** dropdown (checkbox list that overlays the map, with Clear/All and a count badge) next to the State picker — and the map opens fitted to the whole of India, including all of J&K and Ladakh.
- **Pin click**: fetches a photo from Wikipedia (via the `wiki` field) and shows it in the popup.
- **Trip planner**: every popup has **+ Add to trip**. The **Trip** button in the sidebar opens your itinerary. Stops are numbered on the map and joined by a dashed route. You can reorder or remove stops, use **Shortest order** to reorder by distance, see straight-line distances for each leg and in total, and share it as a link (`#trip=…`) or email it. The trip is saved in the browser's localStorage.

## Adding places (scaling to 10k+)

### Quick add (one place)
Edit the relevant state file (e.g. `rj.json`) on GitHub, add an entry to its `places` array, commit. Done.

### Bulk add (using the generator)
1. Open `generate-data.py` locally (not currently in this repo)
2. Add entries to the `PLACES` list:
   ```python
   ("Place Name", "category", lat, lng, "STATE_CODE", "Description", "Wikipedia_Article", True/False),
   #                                                                                       ^ highlight?
   ```
3. Run `python generate-data.py` — it regenerates all files in `data/`
4. Copy the regenerated files into the repo root and commit (the site loads state files from the root, falling back to `states/`)

### Field reference

| Field     | Required | Notes |
|-----------|----------|-------|
| name      | ✔ | Display name |
| cat       | ✔ | `scenic` `religious` `fauna` `history` `arts` `cuisine` `adventure` `festivals` |
| lat, lng  | ✔ | Coordinates |
| stateCode | ✔ | Two-letter code (see `generate-data.py` for the full list) |
| state     | ✔ | Full state name |
| desc      | ✔ | One-line description |
| wiki      | opt | Wikipedia article title → auto-fetches photo |
| img       | opt | Direct image URL → overrides wiki photo |

### Highlight vs. detail
Set `highlight=True` in the generator for places that should appear at the country zoom level. Everything else loads only when users zoom into that state or select it from the dropdown.

## Changing contact email
Edit `CONTACT_EMAIL` in `index.html` (line ~3 of the script block).
