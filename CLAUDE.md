# Simmer

iPad-first cooking companion PWA: a step-by-step timeline with per-step timers, a "serve at"
time that back-computes the start time, a paste-your-recipe importer, and a device-local recipe
library with JSON export/import. Live at https://mrsuperchris.github.io/simmer/.

## Layout

Everything served lives in `docs/`. No build step, no dependencies, no tests.

- `index.html` — the whole UI, one file.
- `app.js` — the sample recipe (lemon & zucchini penne), timeline, timers, recipe importer.
- `library.js` — loads after `app.js` and extends it: saved library, session restore, backups,
  service worker registration. It reuses `app.js` globals (`steps`, `timers`, `$`, ...).
- `sw.js` — network-first cache (`simmer-v2`); falls back to cache only when offline.
- `cooking.png` — 2.6 MB 3x2 sprite of illustrated "cook's-eye" photos, sample recipe only
  (`photo` index picks the cell via background-position).

Both JS files are dense, near-minified single lines. Read them with care before editing.

## Run

```
python -m http.server 8090 --directory docs
```

Then open http://localhost:8090/. Service workers only register on HTTPS or localhost.

## Deploy

GitHub Pages, legacy build, source **main /docs** (checked via `gh api repos/MrSuperChris/simmer/pages`,
2026-10-09). A push to main is live within a minute or two. Simmer is unlisted in
`automation/tiers.json`, so it is tier1: work on `claude/*` branches, Chris merges.

## Data

All user data is in the browser's localStorage, per device and per origin:
`simmer.library.v1` (recipes) and `simmer.session.v1` (cooking progress, timers). Changing either
key, or the app's URL, strands existing users' recipes. Keep the keys stable or migrate them.

## Surprising

- Origin unknown: two commits on 2026-09-13 authored as MrSuperChris, no Claude trailer, not
  built by Claude Code on this machine, and Chris doesn't remember making it. The first local
  clone was made 2026-10-09.
- `app.js` registers a `get_cooking_plan` tool via `document.modelContext.registerTool`
  (the WebMCP draft API) when the browser offers it.
- The committed text files have mixed line endings (one CRLF each, the rest LF), and this
  machine has `core.autocrlf=true`. Check `git diff --stat` before committing so a line-ending
  rewrite of every file doesn't ride along with a small change.
