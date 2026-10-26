# Seal Bay Story Map

An interactive, scrolling story map of the **Seal Bay Baseline Report (v1.0)**, by Spatial Design Hub and Momentum Transport Consultancy, working together.

It runs through 24 chapters, from the regional setting and the internal network through connectivity, accessibility and walking analysis, the site visit and guest profile, to day and night routes for families and older couples, the overlapping corridors, journey experience, priorities and possibilities.

## What's in this repository

| Path | What it is |
|---|---|
| `index.html` | The story map, using the free, open **OpenFreeMap** base map (no API key). It's fully self-contained, so it works on GitHub Pages, from a local drive or as an email attachment. Offline, it falls back to a built-in base map drawn from the project data. |
| `seal-bay-story-map-share.html` | A copy of `index.html` with a descriptive name, for emailing. |
| `maptiler.html` | The same story map on your MapTiler custom style (needs the MapTiler key). |
| `preview/index.html` | The same story map with a built-in base map drawn from the project street network. It needs no MapTiler key, and is useful for offline review. Keep `maplibre-gl-csp-worker.js` next to it. |
| `source-data/` | The GeoJSON layers used to build the map: areas, POIs, catchments, the H3 grid, space syntax, network, routes, desire lines and overlaps. |
| `scripts/` | Build scripts: `prep.py` processes the GeoJSONs into the page data, `build.py` assembles the HTML, and `template.html` is the page source. |

All the data, images and styles are embedded in each HTML file. `index.html` also embeds the map library, so the only things it fetches online are the OpenFreeMap tiles and Google Fonts. `maptiler.html` and `preview/` load the map library from a CDN.

## Publishing on GitHub Pages

1. Create a new repository and upload the contents of this folder, with `index.html` at the top level.
2. Go to **Settings → Pages**, set **Source** to *Deploy from a branch*, and choose `main` and `/ (root)`.
3. The site is published at `https://<your-account>.github.io/<repository-name>/`.

## Base maps and API keys

`index.html` uses OpenFreeMap (https://openfreemap.org), which is free and needs no key. Its map data is © OpenStreetMap contributors. To use a different OpenFreeMap style, change `OFM` in `scripts/build.py` (options: `liberty`, `bright`, `positron`, `dark`, `fiord`).

`maptiler.html` contains the MapTiler style URL with its API key, which every web map exposes in the page. In your MapTiler account, **restrict the key to your GitHub Pages domain** (for example `your-account.github.io`) so it can't be used elsewhere.

To change the style or key, search `index.html` for `api.maptiler.com` and replace the URL, or edit `STYLE` in `scripts/build.py` and rebuild.

## Rebuilding after a data change

The scripts need Python 3 (with `shapely`, `numpy`, `pillow` and `pymupdf`) and Node (with `maplibre-gl@4.7.1`, `lucide-static@0.453.0`, `world-atlas@2.0.2`, `topojson-client@3.1.0` and `@geo-maps/earth-lands-10m@0.6.0`). The paths at the top of `prep.py` and `build.py` point to the original working folders and will need updating to `source-data/`. The report PDF is also needed for the slide images used in chapters 08, 09 and 22–24.

## Notes

- **Desire line and walking times** shown on the route maps are the figures printed in the report.
- **Chapter 07 photo pins** are placed approximately.
- **Coastline** in the preview version: © OpenStreetMap contributors (via geo-maps). In `index.html`, the base map is © MapTiler © OpenStreetMap contributors.
