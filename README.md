# 2026 World Cup · Sticker Tracker

A tiny, installable web app for tracking the stickers still missing from a 2026 World Cup album.
Tap a sticker when you get it. Progress is saved on the device automatically.

- **No build step, no dependencies.** Everything lives in `index.html`.
- **Works offline** once opened (service worker).
- **Installs to the iPhone Home Screen** like a native app.
- **Persistent** via `localStorage`, with JSON export / import for backups.
- **Share your missing list** as plain text: native iOS share sheet, clipboard, or a `.txt` download.

## Run it

Open `index.html` in any browser. That's it.

For the offline cache and Home Screen install you need it served over HTTP(S). Locally:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Put it on your iPhone (easiest path: GitHub Pages)

1. Merge this branch into `main`.
2. In the repo go to **Settings → Pages** and set **Source: GitHub Actions**.
   The workflow in `.github/workflows/pages.yml` publishes the site on every push to `main`.
3. Open the published URL in **Safari** on your iPhone.
4. Tap **Share → Add to Home Screen**.

The Home Screen version runs full-screen with its own icon. Note that iOS gives the Home
Screen app its own storage, separate from Safari, so do your collecting in one place. If you
need to move progress between the two, use **Settings → Export backup** and **Import backup**.

Netlify or Vercel work too: point them at this repo, no build command, publish directory `/`.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app: sticker data, styles, logic |
| `manifest.webmanifest` | Installable web-app metadata |
| `sw.js` | Offline cache (network-first, so updates land immediately) |
| `icons/` | App icons (generated, no branding) |
| `.github/workflows/pages.yml` | Deploys to GitHub Pages on push to `main` |

## Editing the sticker list

The list is the `TEAMS` array at the top of the `<script>` in `index.html`.
Each entry is `{ code, name, flag, ids }`. Totals, percentages and team progress are all
derived from that array, so nothing else needs to change. Saved progress is keyed by sticker
ID, so adding or removing stickers never corrupts existing progress.
