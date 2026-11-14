# BharatYatra — Interactive India Travel Map

A travel planner for India: 650+ curated places (and growing) across 8 categories and 36 states/UTs, with marker clustering, state-level lazy loading, Wikipedia photos, and a vintage-atlas map.

## Deploy in 5 minutes (GitHub Pages)

1. Create a new GitHub repository (e.g. `bharatyatra`)
2. Upload the entire folder structure:
   ```
   index.html
   india-boundary.geojson
   highlights.json
   states-index.json
   slides.json
   airports.json, railway-stations.json
   rj.json, kl.json, up.json, ... (34 state files, all in the repo root)
   ```
3. Go to **Settings → Pages → Source** → select `main` branch, `/ (root)` → Save
4. Live at `https://YOUR_USERNAME.github.io/bharatyatra/`

## How it works

- **Country view**: shows every place (all state files load at start), clustered into coloured groups so the map stays clean even with thousands of pins.
- **Zoom into a state**: the site auto-loads that state's full dataset (lazy). A dropdown also lets visitors pick a state directly.
- **Category pills + State dropdown**: work together as filters. Both update the sidebar list and map markers.
- **On phones**: the controls collapse into one compact row — a **Categories** dropdown (checkbox list that overlays the map, with Clear/All and a count badge) next to the State picker — and the map opens fitted to the whole of India, including all of J&K and Ladakh.
- **Pin click**: opens a photo card — the photo comes from Wikipedia (via the `wiki` field) — with Directions (Google Maps), Wikipedia and **Suggest edit** (emails a correction) links and **+ Add to trip**. Sidebar cards also have a one-tap add-to-trip button.
- **Highlights & Must-do stories**: the ✦ **Highlights** button in the header (and the round **Must-do** chips under the categories) opens a full-screen, swipeable story viewer with 9 decks — *Highlights of India* plus a must-do set for every category (86 slides). Each slide has a big Wikipedia photo, a one-liner, the state, the best season, **Show on map** and **+ Add to trip**. Swipe or tap left/right (phones), ←/→ keys or the arrow buttons (desktop); slides auto-advance with progress bars (press and hold, or Space, to pause); swipe down or Esc to close. First-time visitors get a small teaser card on the map. Decks live in `slides.json` (`{decks:[{id,title,kicker,cat?,slides:[{key:"SC|Place name",line,season,title?,wiki?}]}]}`) and every slide points at a real place on the map; link straight to a deck with `#story=<id>` (e.g. `#story=adventure`).
- **Best in <month> & state stories**: two decks are built in the browser from the data. **Best in <month>** (the calendar chip at the front of the Must-do row, or the second tab in the viewer) picks ~16 places whose `best` time includes that month — short-window festivals first (tagged *Only in Dec* / *Short season*), then curated and highlighted places, at most 2 per state and 4 per category; after the 20th it shows next month, and ‹ › in the viewer flips months. Pick a state and a **▶ Stories** button appears beside the state menu: it plays up to 12 of that state's places (curated slides first). Deep links: `#story=season-dec`, `#story=state-kl`.
- **Surprise me**: the green 🎲 **Surprise me** button at the top right of the map rolls a random real place (only places with a photo; must-dos and highlights come up a little more often, and it won't repeat a recent pick, the same category or the same state twice in a row). Names flicker past like a slot machine, the map flies to the place and a photo card shows its one-liner, best time, **Explore** (zooms in and opens its popup), **+ Add to trip** and **Again**.
- **Getting there (air & rail)**: every popup shows the *nearest airport* (IATA code, e.g. AGR, with a Google Flights search link) and the *nearest major railhead* (Indian Railways code, e.g. AGC, with Google Maps public-transport directions), each with a straight-line "~km"; island places say there is no rail link. Sidebar cards and the Surprise me card show the same codes compactly. The **Airports / Rail** toggles under Surprise me add plane and train markers (majors only on the all-India view, all of them once zoomed in). Data: `airports.json` (`{airports:[{iata,name,city,lat,lng,major?}]}`) and `railway-stations.json` (`{stations:[{code,name,city,lat,lng,major?}]}`), checked against Wikipedia; no routes, schedules or fares are implied.
- **Landing teaser**: first-time visitors get a *Highlights of India* teaser on the map; returning visitors get that month's *Best in <month>* teaser once per month.
- **Trip planner**: every popup and sidebar card can add a place to your trip. The **My trip** tab shows the itinerary as a timeline: a summary card (stops, road km, drive time), numbered stops in order, and each leg's road distance and drive time (or straight-line distance for sea legs). On the map, stops are numbered pins in their category colour (kept out of clusters), and hovering a stop in the list highlights its pin; on desktop the filters fold into one line while the trip is open. Drag stops by their number to reorder (or use the ↑/↓ buttons or arrow keys), remove stops, use **Shortest order** to reorder by distance, and share it as a link (`#trip=…`) or email it. The trip is saved in the browser's localStorage. Longer trips are split into **driving days** (Day 1, Day 2 …, overnight stops marked) using a daily drive limit you choose (4/6/8 h).
- **Design my trip** (itinerary designer): the **Design my trip** button in the header (or in an empty My trip panel; link straight to it with `#design`) asks six questions — days (3–14), month, starting city (or *Anywhere*: the best area for that month), interests (categories), pace (relaxed/balanced/packed → 4/6/8 h max driving a day) and getting around (road, + trains, + flights, or a mix). It builds a day-by-day plan only from places on the map that are in season that month (their `best` field; festivals only in their month), keeps each day's driving under the pace's limit (rough estimate: straight-line × 1.3 at 45 km/h), and on longer trips spends a travel day on a train or flight to a strong new area — only where My trip itself would offer that fly/train leg (nearest airports/stations, no invented routes). **Shuffle** gives another plan; **Open in My trip** loads it with nights per stop, the chosen pace and the train/flight legs, ready to edit, share (`&n=` carries nights per stop) and email. In My trip, overnight stops have −/+ buttons to change the number of nights.
- **Road distances**: each trip leg shows road distance and an estimated drive time from the free public OSRM router (OpenStreetMap data), and the road route is drawn on the map. Island legs or legs with no road fall back to straight-line distance.
- **Map labels**: state and city names are drawn above the pins in warm cream type with a soft dark halo (readable on any satellite imagery) and decluttered on every zoom, so they never hide under a pin or cluster; state/UT capitals carry a saffron ring and New Delhi a filled saffron marker; the six metros are named even on the zoomed-out phone view.
- **Basemap**: satellite only — key-free Esri World_Imagery at every zoom, with neighbouring countries under a deep veil and India's boundary drawn as a cream line with a saffron glow. The imagery shows no borders, so India's official boundary from `india-boundary.geojson` is the only one drawn. It includes all of J&K and Ladakh, and every island group: Lakshadweep, the Andaman & Nicobar Islands (incl. Barren and Narcondam) and Pamban/Rameswaram.
- **Site icon**: `favicon.svg` (saffron-to-terracotta tile with a cream map pin on a green strip), `apple-touch-icon.png` (180 px) and a terracotta `theme-color` for mobile browser chrome.

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
| best      | opt | Best time to visit, e.g. `Oct–Mar` → "Best time" chip |

### Highlight vs. detail
Set `highlight=True` in the generator for places that should appear at the country zoom level. Everything else loads only when users zoom into that state or select it from the dropdown.

## Changing contact email
Edit `CONTACT_EMAIL` in `index.html` (line ~3 of the script block).
