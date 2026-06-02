# classical-music-history — Project Guide

Interactive Western classical music history. Pure frontend (static HTML + vanilla JS + JSON). No framework, no build step.

## Architecture

- `index.html` — landing page. Renders the period timeline and composer navigation.
- `composer.html` — composer detail page. Reads `?id=<composer>` and fetches `data/<id>.json`.
- `data/*.json` — single source of truth. One file per composer (bio, period, works). `composers_list.json` is the ordered index. `spotify_canonical_map.json` maps each work to one canonical Spotify track.
- `js/canonical-spotify.js` — injects the Spotify links at render time.
- `scripts/*.py` — offline helpers that rebuild the Spotify map; not part of the runtime.

## Conventions

- **Content is Chinese, code is English.** Composer names/bios are in Chinese (`name`) with an English field (`nameEn`). All identifiers, keys, and code stay English.
- **Data-driven.** Add or edit a composer by editing JSON only — never hardcode composer data into the HTML.
- **No dependencies.** Keep it vanilla. Don't introduce a bundler or framework unless there's a concrete reason.

## Adding a composer

1. Create `data/<id>.json` following the existing shape (`id`, `name`, `nameEn`, `years`, `period`, `periodEn`, `avatar`, `brief`, `works`).
2. Insert `<id>` into `data/composers_list.json` at the correct period position.
3. If works need Spotify links, add them to `spotify_canonical_map.json` (or rerun the scripts).

## Running

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

Serve over HTTP rather than `file://` so `fetch()` of the JSON data works.
