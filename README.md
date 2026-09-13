# Simmer

An iPad-first cooking companion with a device-local recipe library.

## Features
- Add recipes manually or paste numbered recipe instructions, then review and save.
- Search by name or ingredient, edit, favorite, and delete recipes.
- Export JSON backups and import them without replacing existing recipes.
- Save cooking progress and timers across reloads on the same device and origin.
- Sample recipe with generated cook's-eye images; custom recipes use text guidance and editable sequential timings.

## Run
Serve `docs/` using any static web server. No build or dependencies are needed.

## GitHub Pages
In repository Settings > Pages, select Deploy from a branch, then main and /docs. GitHub Pages from a private personal repository requires GitHub Pro. The published app is public; recipe data stays on each device.

Open the HTTPS Pages address in iPad Safari, then Share > Add to Home Screen. Offline app caching requires HTTPS (or localhost) and a successful initial online visit. The LAN HTTP preview does not support service workers on iPad.

## Data and limits
Recipes are stored in localStorage, not GitHub. Export backups before clearing browser data or changing the app address. Data does not automatically sync. AI parsing, image generation for custom recipes, and cloud accounts are not connected. Timers use wall-clock deadlines, but audible/background alerts while iPad is locked are not implemented. Keep the app visible while cooking.

## Validation
Checked creation, editing, search, favorites, and recipe/progress restoration after reload in the browser. Static JavaScript syntax checked. Full offline installation and background behavior need verification on the hosted HTTPS app.
