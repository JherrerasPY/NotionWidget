# NotionWidget

## Overview
Collection of small, embeddable widgets for Notion (progress bars, trackers, etc).
Each widget is a standalone static page, hosted publicly on GitHub Pages, embedded into Notion via the `/embed` block. Notion requires a public HTTPS URL that doesn't block iframing (no `X-Frame-Options: DENY` / restrictive `frame-ancestors`) — GitHub Pages works fine here.

## Stack
- Plain HTML/CSS/JS per widget, no framework, no build step, no dependencies.
- Config via URL query params (e.g. `?value=75&label=Reading&color=%2300c853`) — no backend, no auth for v1.
- Keep each widget page tiny: inline critical CSS, defer non-essential scripts.

## Structure
- `widgets/<widget-name>/index.html` — one self-contained folder per widget. This is the ONLY file that gets pasted into Notion's `/embed` block — keep it controls-free and minimal.
- `widgets/<widget-name>/builder.html` — optional configurator page for that widget (form + live iframe preview of `index.html` + copy-URL button). Never embedded into Notion itself; it's just a tool for generating the embed URL. Add one once a widget has enough params that hand-editing the URL is annoying.
- `shared/` — CSS/JS reused across multiple widgets (only extract once 2+ widgets actually share it)

## Hosting
- GitHub Pages, served from `master` branch root: repo is `github.com/JherrerasPY/NotionWidget` (public — required for free Pages).
- Each widget's public URL: `https://jherreraspy.github.io/NotionWidget/widgets/<widget-name>/index.html`
- Builder (if present): `https://jherreraspy.github.io/NotionWidget/widgets/<widget-name>/builder.html`

## Progress bar params
`widgets/progress-bar/index.html?...`
- `mode`: `value` (default) | `year` | `daterange`
- `value` (0–100, for `mode=value`), `year` (for `mode=year`, defaults to current year), `startDate`/`endDate` (ISO `YYYY-MM-DD`, for `mode=daterange`)
- `label`, `color` (hex, no `#`), `showPercent` (`true`/`false`), `showCountdown` (`true`/`false`, date modes only — renders a live "Xd Xh Xm Xs left" line below the bar, ticking every second; shows "Completed" once past the end date)
- `font`: `default` | `serif` | `mono` | `rounded` | `condensed` (system font stacks only — no external font loading)
- `size`: `thin` | `medium` (default) | `thick` (bar thickness)

## Conventions
- Every widget must render sensibly with zero query params (sane defaults).
- No comments/docstrings/type annotations on generated code unless the logic is genuinely non-obvious.
- Don't add a backend, build tooling, or framework until a widget actually needs dynamic/live data.

## Response style
- Concise, no preamble/trailing summaries, markdown links for file references.
