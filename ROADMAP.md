# BharatYatra roadmap

## Priority backlog (from Utkarsh, 2026-10-18)
- [x] **Zoomed-in map asked for an API key** — replaced CARTO tiles with key-free Esri tiles (World_Terrain_Base for the overview, World_Imagery satellite from zoom 11, plus a Map/Satellite toggle). Neither draws borders or labels, so `india-boundary.geojson` is the only boundary shown. *(2026-10-18)*
- [x] **Road distances between trip stops** — each leg now shows road km and estimated drive time from the public OSRM server (no key), with the road route drawn on the map. Legs to/from Andaman & Lakshadweep, or with no road, fall back to clearly labelled straight-line distance. Results are cached per leg; requests are debounced. *(2026-10-18)*
- [x] **Visual refresh, pass 2 — popups & sidebar** — popups are now photo-led cards: 168px Wikipedia photo with a shimmer while it loads and a fade-in, place name and state set over the photo, category chip, a coloured header when there's no photo, and a soft pop-in animation. Each popup has Directions (Google Maps), Wikipedia and **Suggest edit** (email to utkarsh.khurana@outlook.com) links. Popups size to the screen and no longer slide under the map controls on phones. Sidebar cards got larger category tiles, a category + state line, 2-line descriptions, hover lift, a highlight for the place whose popup is open, and a one-tap **+ / ✓ Add to trip** button. Fixed Neer Mahal's coordinates (23.50, 91.32). *(2026-10-18, run 2)*
- [x] **Visual refresh, first pass** — terrain basemap, misted neighbours with a warm wash inside India, saffron-halo boundary, teardrop category pins, cream clusters with coloured rings, tricolour header rule, serif state labels, less clutter on phones. *(2026-10-18)*

## Next
- Visual pass 3: header and category filter polish (desktop pills → compact grid, sticky search), a trip panel restyle (timeline look for legs), and a check of the whole look on real Esri tiles on a phone.
- Check pins that fall just outside the simplified boundary.
- Lazy photo thumbnails in the sidebar cards (only for cards scrolled into view).
- More Adventure places (real, well-known treks and rafting spots).
