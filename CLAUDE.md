# Apex Athlete

Will's personal training app: a phone web app (PWA) hosted on GitHub Pages and installed on his iPhone home screen. Spun off from the health and fitness parts of Apex Life OS.

## How it's built
- **One file does everything: `index.html`**, with inline CSS and plain JavaScript and no build step. Edit it directly.
- `sw.js`: the service worker (offline cache). Bump the `V` version string whenever `index.html` changes so phones pick up the update.
- `manifest.webmanifest` and the icons: install metadata.
- **Data lives on the phone** in IndexedDB (database `apex-athlete`, store `kv`, keys `state` and `settings`), with a localStorage copy as a fallback. Settings > Backup exports and imports the whole state as JSON. Don't rename the database or keys, or existing data is lost.
- **AI:** Anthropic Messages API called from the browser with the user's own key (header `anthropic-dangerous-direct-browser-access`), streamed. `claudeCall()` is the single entry point; `SAMPLE()` / `SAMPLE.json()` wrap it. Default model `claude-sonnet-5-5`; the coach chat uses `claude-haiku-4-5-20251001`.
- Every AI feature has an offline example fallback, shown when no key is set or on request after an error.

## Main areas
- Today, Train (programme, Train Like A x24, PBs with rep maxes and estimated/actual 1RM, history), Fuel (diary, Eat Like A x10 meal plans, supplements), Sport (only when the user has added a sport: roadmap, skills, focus, log for 30 disciplines), Progress (free-text goal plans, body).
- Interactive workout player with rest and work timers, exercise swaps and a screen wake lock.
- Sign-up runs on first launch; sports are optional.
