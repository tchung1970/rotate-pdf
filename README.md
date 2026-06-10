# Rotate PDF

A single-page web app to upload a PDF, rotate any/all pages, and download the result.
Live at: https://ai.tchung.org/rotate-pdf/

| Before | After |
|:------:|:-----:|
| ![Page sideways](docs/cert-before.png?v=2) | ![Page upright](docs/cert-after.png?v=2) |

## Why
Adobe quietly paywalled page rotation in the free Acrobat Reader in late 2021.
Since then, "Rotate Pages" requires a paid Acrobat Pro subscription. Built this free,
browser-based alternative instead of subscribing just for that — it rotates and saves
any page, all locally.

## How it works
- **100% client-side** — the PDF never leaves the browser (no upload, no backend,
  no size limit, no server load).
- `pdf.js` renders page thumbnails; `pdf-lib` writes the rotated output by setting
  each page's rotation metadata (no re-rasterizing, so original quality is kept).
- Output filename: `<original>-rotated.pdf`.

## Features
- Drag-and-drop or click-to-browse upload
- Per-page rotate left / right (90° steps)
- "Rotate all 90°" and "Reset" buttons
- Large, centered, high-resolution page previews (render scale 1.5, ~320px tall)

## Run locally
The app is one self-contained file with no build step. Either:

- **Just open it** — double-click `index.html` (it loads its two libraries from a CDN,
  so the browser needs internet access), or
- **Serve it** from this directory, e.g.:

      python3 -m http.server 8000
      # then visit http://localhost:8000/

## Files
- `index.html` — the entire app (HTML + CSS + JS inline).
- `docs/` — `cert-before.png` / `cert-after.png` screenshots used in this README,
  and `example.pdf`, a sample one-page PDF to try the rotator on.

## Dependencies (loaded from CDN at runtime)
- pdf-lib 1.17.1  (cdnjs)
- pdf.js 3.11.174 (cdnjs)

Requires internet access in the visitor's browser. To make it fully self-contained,
vendor these two libraries into this directory and update the `<script>` src paths.

## Deploy
Static file, no backend or special nginx config needed (served by a default
`location /` static block). For example, the live site is served from
`/var/www/html/rotate-pdf/` and updated by copying the file up to the host:

    scp index.html user@your-server:/var/www/html/rotate-pdf/

## License
[MIT](LICENSE) © Thomas Chung
