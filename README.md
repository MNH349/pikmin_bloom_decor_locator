# Pikmin Decor Finder · Taipei

A mobile web app that shows which real-world sites in Taipei will give which
**Decor Pikmin** in Pikmin Bloom. It reads live OpenStreetMap data (the same
source Niantic derives decor from) and maps each point of interest to its decor
type — handling priority correctly (e.g. a restaurant tagged `cuisine=sushi`
resolves to **Sushi**, not the generic **Restaurant**).

## Features
- Interactive Leaflet map centered on Taipei
- Filter by a specific decor type, or show **All** decor at once (color-coded)
- Tap a pin → decor type, venue name, the matched OSM tag, and Apple/Google Maps directions
- "Search this area" re-queries wherever you pan/zoom; 📍 button jumps to your location
- Installable to the iPhone home screen (PWA)

## Files
- `index.html` — the whole app (decor↔OSM mapping + map + Overpass queries)
- `manifest.webmanifest`, `icon.svg` — home-screen install metadata

## Run it on your iPhone

### Easiest: GitHub Pages (free, permanent URL)
1. Create a public GitHub repo and upload these files to the root.
2. Repo **Settings → Pages → Source: `main` / root**, save.
3. Open the resulting `https://<you>.github.io/<repo>/` URL in **Safari** on your iPhone.
4. Share button → **Add to Home Screen**. It now opens full-screen like an app.

### Quick local test (phone on same Wi-Fi as this Mac)
```bash
cd pikmin-decor-taipei
python3 -m http.server 8777
```
Then on your iPhone open `http://<your-mac-LAN-IP>:8777/index.html`
(find the IP with `ipconfig getifaddr en0`).

## How the decor mapping works
The mapping in `DECOR_RULES` (top of `index.html`) comes from
<https://www.pikminwiki.com/Decor_Pikmin>. Rules are ordered by specificity and
the **first** matching rule wins, so cuisine-specific decors (Sushi, Ramen,
Italian, Curry, Mexican, Korean) take priority over generic Restaurant/Fast-food.
To adjust a mapping, edit that array — no other code changes needed.

## Accuracy caveat
This predicts decor from the **same OSM data** the game uses, but Niantic runs
its own periodic snapshots and undocumented tie-breaking. It's right the large
majority of the time but isn't a guaranteed 1:1 with live game state. It also
can't see brand-new OSM edits until they propagate.

## Notes / limits
- Uses the free public **Overpass API**. "All decor" over a dense area is a
  heavy query (~15s) and the public server occasionally throttles — just tap
  "Search this area" again. Single-decor searches are fast.
- Requires zoom level ≥ 13 before it searches, to keep queries reasonable.
