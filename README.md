# Harlow's Accidental Journey — Artwork Review

> A picture book by Lois Farrell — the family review site for finished spreads, cover options, title treatments, and the character cast.

**Branch policy:** work happens on the latest *-vN / project branch. List branches before editing. Never assume the GitHub default is the working line. Working line: `Harlows-v2` (GitHub default is `main`). `Harlows-v1` is the frozen restore point for the dialed-in Oct 9 build — do not commit to it. `main` is the published branch, synced from `Harlows-v2`.

[![Preview](https://img.shields.io/badge/Preview-Live-brightgreen)](https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/)
[![GitHub Pages](https://github.com/MyDigitalStudioz/Harlows-Accidental-Journey/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/MyDigitalStudioz/Harlows-Accidental-Journey/actions/workflows/pages/pages-build-deployment)
![Last commit](https://img.shields.io/github/last-commit/MyDigitalStudioz/Harlows-Accidental-Journey)
![Repo size](https://img.shields.io/github/repo-size/MyDigitalStudioz/Harlows-Accidental-Journey)
![Static site](https://img.shields.io/badge/site-static-blue)
![Version](https://img.shields.io/badge/version-1.0.0-orange)

## Live preview

https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/

![Artwork review site](media/hero.jpg?v=1)

## What's inside

- **Finished Spreads** — pages 1–6 in a click-through lightbox; finished spreads include a *Read text* popup with the locked copy
- **Cover Options** — wraparound favorite plus front/back options B, D, and E
- **Welcome Page Options** — three directions for the book's opening page
- **Front Cover Mock-ups** — 8 title treatments on real covers in a 3D drag-and-flip deck, plus a collapsible logo-only comparison strip
- **Meet the Cast** — all 41 approved character portraits in a searchable grid
- **Documents** — Jon's and Lois's storyline PDFs, view or download
- Fullscreen image viewer with floating arrows (keyboard ← → supported), sticky section nav, back-to-top button

## Design language

Warm storybook: cream paper (`#faf6ee`), dark cocoa ink (`#3d3229`), burnt-orange accent (`#b3541e`). Georgia serif throughout, soft layered cards, generous whitespace — built to feel like the book.

## Tech stack

| Layer | Choice |
|---|---|
| Markup | Single self-contained `index.html` — no frameworks, no build step |
| 3D deck | Hand-rolled CSS 3D (Deckz pattern): drag, arrows, dots, keyboard |
| Viewer | Custom lightbox: fullscreen image mode, caption arrows, text popups |
| Images | JPG/PNG, `loading="lazy"` throughout |
| Hosting | GitHub Pages from `main` (`.nojekyll`) |

## Project structure

```
Harlows-Accidental-Journey/
├── index.html        # the whole review site
├── media/            # README screenshots + social preview
├── spreads/          # finished spreads, pages 1–6
├── covers/           # wraparound, options B/D/E, 8 cover mock-ups
├── logos/            # 8 isolated title treatments
├── welcome/          # 3 welcome-page options
├── characters/       # 41 approved character portraits
├── docs/             # storyline PDFs (Jon's + Lois's)
└── prompt-pack/      # generation reference images
```

## Screenshots

| 3D cover deck | Meet the Cast |
|---|---|
| ![Cover mock-up deck](media/screenshot-deck.jpg?v=1) | ![Character grid](media/screenshot-cast.jpg?v=1) |
| Drag, flip, or arrow through all 8 title treatments on real covers. | 41 approved portraits, searchable, tap to view big. |

| Mobile |
|---|
| ![Mobile view](media/screenshot-mobile.jpg?v=1) |
| Fully responsive — verified at 390px. |

## Workflow

Changes land on `main` and go live via Pages. Check the branch list before starting new work — if a `*-vN` branch exists for the current round, that's the working line, not `main`.
