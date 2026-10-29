# Ribbon Clock

A sky-as-timeline clock. The page shows a 14-hour window of the sky around now: sun, moon (with phase), Venus, stars, clouds, rain, snow, wind, fog, thunderstorms, temperature and official DWD weather warnings. Drag to scrub through time, double-click to return to now.

Single self-contained file — no build step.

## Publish on GitHub Pages

1. Create a new repository and add `index.html` (and this README) to the root.
2. Repository → Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The clock is live at `https://<user>.github.io/<repo>/` after a minute.

HTTPS (which Pages provides) is required for the browser's location prompt.

## Data sources

- Weather: [Open-Meteo](https://open-meteo.com) — DWD ICON (ICON-D2 where available), fallback to Open-Meteo best match. Free, no key; non-commercial use.
- Warnings: [Bright Sky](https://brightsky.dev) — DWD warnings, Germany only.
- City search: Open-Meteo geocoding.
- Sun, moon and Venus positions are computed locally.

Language follows the browser: German for `de`, English otherwise. Location is taken from the device (if allowed), otherwise from the time zone; a typed city is saved in localStorage.
