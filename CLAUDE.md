# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Hand-written static site (Louise Bernard's personal academic/professional site) deployed via GitHub Pages from `main`. No build step, no package manager, no JS framework, no tests. Edit HTML/CSS and push — that's the entire workflow. Preview locally by opening the `.html` files directly or with any static server (`python3 -m http.server`).

## Architecture

Four sibling pages — `index.html`, `research.html`, `cv.html`, `contact.html` — each a complete standalone HTML document. All four share `assets/style.css` as their only stylesheet. There is no shared layout/include mechanism, so:

- **The header `<nav>` block is duplicated in all four files.** Any nav change (adding a page, renaming a link, updating the brand line) must be applied to every file. The `class="current"` on the active link is what differs between them.
- **The footer is also duplicated** across all four files (currently `© 2026 Louise Bernard` / `London, UK`).
- **Each `<head>` carries its own meta block** (canonical, Open Graph, Twitter Card) and its own JSON-LD structured data. Per-page values differ (title, description, canonical, JSON-LD type), but the canonical domain (`https://louisealice.github.io`) appears repeatedly across all four files. If the custom domain is switched on, that hostname must be replaced everywhere — `<link rel="canonical">`, `og:url`, `og:image`, `twitter:image`, and every `url` / `image` field in the JSON-LD blocks.
- Year/copyright bumps therefore touch four files, not one.

`assets/style.css` is the single source of truth for visual design. Design tokens (colours, fonts, layout widths) live in `:root` custom properties at the top — `--paper`, `--ink`, `--accent` (navy), `--accent-warm` (terracotta, used sparingly), `--serif` (Cormorant Garamond body), `--sans` (Inter UI), `--measure` (prose column width), `--gutter`. Changing these retones the whole site; prefer editing tokens over adding ad-hoc colours/sizes in component rules.

Page-specific CSS sections in `style.css` are clearly demarcated by comment banners (`Home hero`, `Research page`, `CV page`, `Contact page`). New content blocks should reuse existing classes (`.paper`, `.cv-entry`, `.cv-section`, `.contact-block`) rather than introducing new ones.

## Content patterns

- **Add a paper**: copy an existing `<article class="paper">` block in `research.html`. The grid is `5rem 1fr` (year column + content).
- **Add a CV entry**: copy a `<div class="cv-entry">` block in `cv.html` inside the appropriate `<section class="cv-section">`. Grid is `9rem 1fr` (date/label column + content).
- **Portrait fallback**: `index.html` uses an inline `onerror` handler on the portrait `<img>` that swaps in a `.portrait-placeholder` div if the image is missing. Don't remove this — the file is `assets/portrait.jpeg` (note `.jpeg`, not `.jpg` as the README says).
- **Contact form**: posts to Formspree at form ID `xeenwodl` in `contact.html`. If that ID is changed, update the comment block above the form to match.
- **External links**: all use `target="_blank" rel="noopener"`.

## Things not to do

- Don't introduce a build tool, bundler, or templating engine for "DRY"-ing the duplicated header/footer — the site is intentionally hand-edited static HTML. If the duplication becomes painful, raise it with the user before changing the architecture.
- Don't add JavaScript frameworks or dependencies. The only inline JS is the portrait `onerror` fallback.
- Don't rename `assets/cv.pdf` — it's linked from `cv.html` as the downloadable CV.
