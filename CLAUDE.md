# NotionWidget

## Overview
Collection of small, embeddable widgets for Notion (progress bars, trackers, etc).
Each widget is a standalone static page, hosted publicly on GitHub Pages, embedded into Notion via the `/embed` block. Notion requires a public HTTPS URL that doesn't block iframing (no `X-Frame-Options: DENY` / restrictive `frame-ancestors`) — GitHub Pages works fine here.

## Stack
- Plain HTML/CSS/JS per widget, no framework, no build step, no dependencies.
- Config via URL query params (e.g. `?value=75&label=Reading&color=%2300c853`) — no backend, no auth for v1.
- Keep each widget page tiny: inline critical CSS, defer non-essential scripts.

## Structure
- `widgets/<widget-name>/index.html` — one self-contained folder per widget
- `shared/` — CSS/JS reused across multiple widgets (only extract once 2+ widgets actually share it)

## Hosting
- GitHub Pages, served from `main` branch root (or `/docs`, TBD once repo is pushed).
- Each widget's public URL: `https://<user>.github.io/NotionWidget/widgets/<widget-name>/`

## Conventions
- Every widget must render sensibly with zero query params (sane defaults).
- No comments/docstrings/type annotations on generated code unless the logic is genuinely non-obvious.
- Don't add a backend, build tooling, or framework until a widget actually needs dynamic/live data.

## Response style
- Concise, no preamble/trailing summaries, markdown links for file references.
