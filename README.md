# Ribbon Clock

A sky-as-timeline clock. The screen shows 12 hours of the real sky over your location, from 6 hours ago to 6 hours ahead; drag to scrub between −6 h and +48 h, double-click to return to now.

Single self-contained file, no build step.

## Design principles

1. **Show, don't tell.** Cloud cover is shown as clouds, sunlight as light, precipitation as rain.
2. **Encode information naturally.** Brightness, colour, position, density and movement carry the data.
3. **Text only where imagery is insufficient:** time, temperature, warnings, celestial object names.
4. **No redundancy.** If the sky shows it's cloudy, there is no cloud percentage.
5. **Scientific accuracy.** The picture is a visualization of actual data, not an illustration.

## What you see

- **Sky colour** follows the sun's real altitude: night, dawn/dusk, golden hour, daylight. Night mode dims the screen 23:00–06:00.
- **Sun, moon, Venus, stars** at their true altitude; accurate moon phase; real constellations; moonlight fades the stars. Venus is labelled as morning or evening star.
- **Sun and moon paths** are solid and bright where a clear view is likely, thin and dashed where clouds hide them.
- **Clouds in three layers:** fog-like low cloud near the horizon, puffy mid-level cloud, thin cirrus streaks up high. Each follows its own forecast and drifts with the wind.
- **Precipitation** falls from the cloud layer carrying it and lands on the horizon. Drizzle is fine and faint, heavy rain (up to 10 mm/h) dense with longer streaks and small splashes; snow gets denser with intensity.
- **Wind** as streaks, **thunderstorms** as lightning.
- **Temperature** coloured on a warmth scale (violet −15 °C … dark red 40 °C).
- **DWD warnings** as a coloured edge above the affected hours.
- Text switches between light and dark ink to stay readable on any sky.

## Measured "now"

The forecast is corrected with observations, using this hierarchy:

1. **Satellite** (EUMETSAT via Open-Meteo, 10-min, Europe-wide): the clear-sky index (measured ÷ clear-sky sunlight) is treated as evidence of blocked sunlight, not as cloud coverage. Only clearly clear or clearly dimmed values carry full confidence.
2. **Stations**, ranked by distance and elevation difference (not just distance): GeoSphere Austria (TAWES), MeteoSchweiz, DWD via Bright Sky.
3. **ICON-D2** stays the baseline when observations aren't representative.

Rules:
- "Now" uses only readings younger than 60 min, weighted down with age; older readings only reconstruct past hours, at capped weight.
- Blocked-sun evidence and total cloud cover are never averaged together.
- Contradicting sources cut the correction to a quarter; suspected valley fog halves it and discounts stations at other elevations.
- The correction fades back into the forecast over about three hours.
- At night only Germany has a correction (DWD cloud cover); sunshine-based sources need the sun up.

## Location

Device location if allowed, otherwise time zone. The city field suggests places as you type, with elevation (m above sea level); the choice is saved in localStorage. The trash icon returns to device location. The **i** button lists location, elevation and the data sources currently in use.

## Data sources

- Forecast: [Open-Meteo](https://open-meteo.com) — DWD ICON-D2 (15-min precipitation, cloud layers), fallback to best match. Free, no key, non-commercial use.
- Satellite radiation: Open-Meteo satellite API (EUMETSAT).
- Stations: [GeoSphere Austria](https://data.hub.geosphere.at), [MeteoSchweiz](https://www.meteoschweiz.admin.ch) open data, [Bright Sky](https://brightsky.dev) (DWD).
- Warnings: Bright Sky — DWD warnings, Germany only.
- City search and elevation: Open-Meteo geocoding.
- Sun, moon, Venus and stars are computed locally.

Language follows the browser: German for `de`, English otherwise.

## Publish on GitHub Pages

1. Create a repository and add `index.html` and this README to the root.
2. Settings → Pages → Source: "Deploy from a branch", branch `main`, folder `/ (root)`.
3. The clock is live at `https://<user>.github.io/<repo>/` after a minute.

HTTPS (which Pages provides) is required for the browser's location prompt.
