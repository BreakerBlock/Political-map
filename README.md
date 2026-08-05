# BharatYatra — Interactive India Travel Map

A single-page travel planner for India: 145+ curated places across 8 categories, plotted on an interactive map with photos, search, and category filters.

## Deploy in 5 minutes (GitHub Pages)

1. Create a new GitHub repository (e.g. `bharatyatra`)
2. Upload both files to the repo root:
   - `index.html`
   - `places.json`
3. Go to **Settings → Pages → Source** → select `main` branch, `/ (root)` → Save
4. Your site is live at `https://YOUR_USERNAME.github.io/bharatyatra/`

## Updating places (no coding needed)

1. Open `places.json` in your repo → click the ✏️ pencil icon
2. Add a new entry to the `"places"` array:

```json
{"name":"My New Place","cat":"scenic","lat":28.61,"lng":77.20,"state":"Delhi","desc":"One-line description","wiki":"Wikipedia_Article_Title"}
```

3. Commit — the live site picks it up on the next page load.

### Field reference

| Field  | Required | Notes |
|--------|----------|-------|
| name   | ✔ | Display name |
| cat    | ✔ | One of: `scenic` `religious` `fauna` `history` `arts` `cuisine` `adventure` `festivals` |
| lat, lng | ✔ | Right-click a spot on Google Maps → first line shows them |
| state  | ✔ | State or region shown in the popup |
| desc   | ✔ | One-line description |
| wiki   | optional | Wikipedia article title (the part after `/wiki/` in the URL). Used to auto-fetch a photo for the popup |
| img    | optional | Direct image URL — overrides the Wikipedia photo |

### Adding a new category

Add it to the `"categories"` object in `places.json`:

```json
"beaches": { "label": "Beaches & Coast", "color": "#0E7490" }
```

Then use `"cat":"beaches"` in places. (The category will use the default mountain icon unless you add a matching SVG in `index.html` → `ICONS`.)

### Changing your contact email

Edit `meta.contactEmail` in `places.json`. The "Suggest a Place" button opens visitors' email clients with a pre-filled template addressed to it.

## How images work

When a visitor clicks a pin, the site queries the free Wikipedia REST API using the place's `wiki` field and shows the article's lead photo. No image hosting, no API keys. If a place has an `img` URL, that's used instead. If neither yields a photo, the popup simply shows text.
