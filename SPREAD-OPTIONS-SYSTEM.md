# Spread Options system: handoff guide

This guide is for whoever maintains the Harlow's Accidental Journey review pages (Trinity, Folio, Ravyn). It explains how the pages work, how to change them safely, and what never to do.

## Pages

| Page | Live URL | File |
|---|---|---|
| Showcase (top section is "Current favorites") | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/ | `index.html` |
| Spread Options (every version of every spread) | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/spread-options.html | `spread-options.html` |
| Favorites data (read by both pages at load time) | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/favorites.json | `favorites.json` |

Repo: `MyDigitalStudioz/Harlows-Accidental-Journey`, published by GitHub Pages from `main`.
When you send someone a link, add a cache-buster: `...spread-options.html?v=<short-sha>`.
To link to one card, add its letter as an anchor: `spread-options.html#S05-G`. Every card has `id="<letter>"`.

## Cards and letters

- Each spread (S01 to S24) is a `<section id="S05">` on `spread-options.html`. Each version is an `<article class="card" id="S05-G" data-letter="S05-G" data-status="..." ...>`.
- **Letters are append-only.** A new version gets the next free letter at the end of its spread (S05-H after S05-G). Never re-letter, reorder, or reuse a letter. People's picks and links depend on them.
- **The `render:` line** under a letter (`<span class="render-id">render: S05-E</span>`) is the name the picture had when it was first made, before it got its page letter. Add it whenever the two differ. Showcase images say `render: showcase pNN`.
- **Images:** export each version as a **1400×700 JPEG** (2:1) into `spread-options/`, named in lower case after the letter (`spread-options/s05-g.jpg`). Point the card's `<img class="thumb">` `src` and `data-render` at it. `data-print` is for an optional print-ready variant (same spec, `-print` suffix) and is left empty otherwise.
- After adding cards, update the section hint ("N versions, oldest first") and the header total ("163 versions"), and check the card count (see Publish).

## The four labels

Every card has exactly one status, set in both `data-status` and the status chip:

| Label | Chip | Use it when |
|---|---|---|
| **Candidate** | `<span class="status st-cand">Candidate</span>` | A strong option. It could be the one, still being decided. |
| **Option** | `<span class="status st-opt">Option</span>` | Another version of the page to compare, including versions set aside for taste, color, story or canon reasons. |
| **Needs a fix** | `<span class="status st-fix">Needs a fix</span>` | **Fit problems only.** Something important (a face, a paw, a key character or detail) lands in the middle fold, off the page edge (past trim), or under the words (the text band). It's fixable if we like the idea. Never use it for taste, color, finish or canon. Those cards are **Option** plus a plain note. |
| **Jon's yes** | `<span class="status st-yes">Jon&#x27;s yes</span>` | Only after Jon himself has said yes to that exact version. Nobody else sets it on his behalf. |

**Check notes (Candidate cards only),** placed right after the chip and mirrored in `data-check`:

- `<span class="check ck-pass">Checks passed</span>` (green): it fits the page well (fold, trim and text all pass).
- `<span class="check ck-nits">Passed with small fixes</span>` (amber): it fits, with tiny touch-ups if chosen.
- `<span class="check ck-grey">Being checked</span>` (grey): just made and not looked over yet. This is the default for new renders.

**Plain notes:** a card can carry a short reason for Lois, written in plain words, e.g. `<p class="plain-note">Note: coat color off</p>` (placed before the `summary` paragraph). Use one on every Needs a fix card and on any Option card that was set aside for a reason.

The **"What do these labels mean?"** button (in the filter chips; on phones also under the color key) opens the plain-English guide. If you change a label, update the guide panel (`#labelGuide`) too.

Filter chips: All, Candidate, Option, Needs a fix, Jon's yes, plus the favorites filters (Any favorite, 2+ picks, T, F, R, J, L).

## Favorites (`favorites.json`)

```json
{
  "_comment": "...",
  "people": {
    "T": {"name": "Trinity", "color": "#0f766e", "picks": ["S01-I", "S02-D"]},
    "F": {"name": "Folio",   "color": "#7c3aed", "picks": []},
    "R": {"name": "Ravyn",   "color": "#1a1a1a", "picks": []},
    "J": {"name": "Jon",     "color": "#c9a227", "picks": []},
    "L": {"name": "Lois",    "color": "#e11d48", "picks": []}
  }
}
```

- `picks` are **page letters** (as shown on the cards), never render IDs. These are current favorites only, normally one per spread per person. Moving a pick means replacing that spread's letter.
- **Both pages read `favorites.json` at load time.** Editing that one file updates the dots on Spread Options *and* the Current favorites on the showcase. There's no second edit.
- `spread-options.html` also has a baked copy (`const FAVORITES = {...}`) used only as an offline fallback. Keep it in sync when convenient (paste the `people` object), but the live JSON wins.
- **Example: "Mom likes S05-G"** → add `"S05-G"` to `people.L.picks` (remove any other S05 letter from Lois's list), commit `favorites.json`, and publish. S05-G gets a rose **L** dot, and because Lois's pick outranks the desks, the showcase switches S05 to S05-G (unless Jon has an S05 pick, or S05-G is Needs a fix).
- Same for Jon: add the letter to `people.J.picks`. Picks are not labels. If Jon says "yes, that's the one," also set that card to **Jon's yes**.

## Showcase rules ("Current favorites" on `index.html`)

One image per spread that has cards on Spread Options, computed in the browser from `favorites.json` plus the card statuses on `spread-options.html` (`pickShowcase()` in `index.html`). For each spread, in order:

1. **Jon's pick** (J dot).
2. **Lois's pick** (L dot).
3. **Most desk dots** (T/F/R). On a tie, keep the image currently showing (`SHOWCASE_SHOWING` in `index.html`). If that isn't among the tied versions, use Trinity's pick among the tied (then Folio's, then Ravyn's).
4. **No picks:** keep the current showcase image if one exists, otherwise Folio's pick, otherwise skip the spread.

**Eligibility:** a **Needs a fix** card can never be on the showcase. It's skipped, and the next rule applies.

Under each image: the pickers' dots and the page letter, linked to `spread-options.html#<letter>`. Tapping the image opens the big viewer with arrows, as before. "Read text" shows only for spreads that have page text in `spreadText`.

`SHOWCASE_SHOWING` holds the tie-break baseline (currently the six original showcase images, S01-L to S06-H). If you want a tie to stay sticky on a newer winner, set that spread's letter there. Spread titles live in `SPREAD_TITLES`. The old `spreads/p0N-*.jpg` images stay in the repo; they're the offline fallback if the page data can't be fetched.

A reference copy of the rules in Python is at `/workspace/haj-batch/tmp/showcase_pick.py` on the box (run it with the repo path to print the expected picks).

## Publish process

1. Start from current `main` and note its sha. Create a branch (`cursor/<short-topic>`). Commit only the files you meant to change.
2. Push the branch, then **fast-forward** `main` to it (e.g. `gh api -X PATCH repos/MyDigitalStudioz/Harlows-Accidental-Journey/git/refs/heads/main -f sha=<sha> -F force=false`). If `main` moved, rebase or redo your change on the new main; don't overwrite.
3. Wait for the Pages build (`gh api repos/.../pages/builds/latest` → `built <sha>`).
4. Fetch the live file with `?v=<short-sha>` and compare its size/SHA-256 with the committed file.
5. Verify in a browser: the card count is unchanged unless you added cards (count `main article.card`; it's 163 as of 2026-10-15), only the four labels appear, no script errors, and it looks right at 390px wide.
6. Only then share the link, with `?v=<short-sha>`.

## Never

- Never force-push, and never rewrite published history.
- Never touch the `Harlows-v2` branch (or the other `Harlows-v*` branches).
- Never re-letter, reorder, delete or reuse card letters.
- Never use "Banked", "Approved", "locked" or "final" wording on cards or in `favorites.json`. Use "Recommended" for a desk recommendation. Only Jon gives a yes, shown as **Jon's yes**.
- Never use **Needs a fix** for anything but fit (fold, page edge, text band).
- Never put a Needs a fix card on the showcase.
- Never delete the old `spreads/p0N` images.
