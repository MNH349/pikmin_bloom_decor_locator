# Pikmin Decor Finder

A mobile web app that shows which real-world sites will give which
**Decor Pikmin** in Pikmin Bloom. It reads live OpenStreetMap data (the same
source Niantic derives decor from) and maps each point of interest to its decor
type. 

## Features
- Interactive Leaflet map centered on Taipei Main Station (subject to change)
- Filter by a specific decor type, or show all decor at once (color-coded)
- Each searched pin shows the decor type, venue name, the matched OSM tag, and Apple/Google Maps directions
- "Search this area" re-queries wherever you pan/zoom; 📍 button jumps to your location
- Installable on the iPhone home screen as a progressive web app (PWA)

## Files
- `index.html` — the whole app 
- `manifest.webmanifest`, `icon.svg` — home-screen install metadata

## Run it on your iPhone

### Easiest: GitHub Pages (free, permanent URL)
1. Open the **Safari** on you iPhone and use this URL: `https://mnh349.github.io/pikmin_bloom_decor_locator/`
2. Share button → **Add to Home Screen**. It now opens full-screen like an app.

## How the decor mapping works
The mapping in `DECOR_RULES` (top of `index.html`) comes from
<https://www.pikminwiki.com/Decor_Pikmin>. Rules are ordered by specificity and
the **first** matching rule wins, so cuisine-specific decors (Sushi, Ramen,
etc.) take priority over generic restaurants (Chef Hat).

## Notes / limits
- Uses the free public **Overpass API**. The search time depends on the server speed of OSM
  - v9 uses parallel querying and caching to improve search speed, but ultimately still depends on the server
- Suggests zoom level ≥ 16 (default) before it searches, to keep queries reasonable.
- The newer version of the app will be automatically deployed if you save it on the home screen
