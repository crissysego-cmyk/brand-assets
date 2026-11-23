# Repository notes

## What this repo is

This repository was imported from `crissysego-cmyk/brand-assets`. Commit `51c7f40` ("Add Brand Assets") added only design assets — `Logos/**` (27 SVG/PNG/JPG files across three lockups) and `Verifier Alliance.pdf` (brand guidelines) — with **no application code**. That is why the update could not start: there was nothing to build or run.

## What was added to make it run

- `index.html` / `styles.css` — static brand asset library listing every logo variant with SVG/PNG/JPG downloads, brand colours and a link to the PDF.
- `server.js` — zero-dependency Node static server on port 3000 with correct MIME types, URL-decoded paths (asset filenames contain spaces) and an SSE live-reload endpoint (`/__reload`) watching `.html/.css/.js/.svg`.
- `docker-compose.base44.yml` — `web` service on `node:22-alpine`, source bind-mounted at `/app`, runs `node server.js`, healthcheck via `fetch` on `/`.

## Run and verify

```bash
docker compose -f docker-compose.base44.yml up -d --build
curl -s http://localhost:3000/ | head
```

No dependencies to install, no build step, no tests, no database. Asset filenames contain spaces — always URL-encode them (`%20`) in HTML links.
