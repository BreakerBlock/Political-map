# BharatYatra roadmap

## Priority backlog (from Utkarsh, 2026-10-18)
- [x] **Zoomed-in map asked for an API key** — replaced CARTO tiles with key-free Esri tiles (World_Terrain_Base for the overview, World_Imagery satellite from zoom 11, plus a Map/Satellite toggle). Neither draws borders or labels, so `india-boundary.geojson` is the only boundary shown. *(2026-10-18)*
- [x] **Road distances between trip stops** — each leg now shows road km and estimated drive time from the public OSRM server (no key), with the road route drawn on the map. Legs to/from Andaman & Lakshadweep, or with no road, fall back to clearly labelled straight-line distance. Results are cached per leg; requests are debounced. *(2026-10-18)*
- [x] **Visual refresh, first pass** — terrain basemap, misted neighbours with a warm wash inside India, saffron-halo boundary, teardrop category pins, cream clusters with coloured rings, tricolour header rule, serif state labels, less clutter on phones. *(2026-10-18)*

## Next
- Visual pass 2: refine the sidebar cards and popups (bigger photos, smoother open/close), check the look against real tiles on a phone.
- Check pins that fall just outside the simplified boundary; fix Neer Mahal (Tripura) longitude (~91.32).
- "Suggest an edit" link in each popup → email to utkarsh.khurana@outlook.com.
- More Adventure places (real, well-known treks and rafting spots).
