# Spread Options system: handoff guide

This guide is for whoever maintains the Harlow's Accidental Journey review pages (Trinity, Folio, Ravyn). It explains how the pages work, how to change them safely, and what never to do.

## Pages

| Page | Live URL | File |
|---|---|---|
| Showcase (top section is "Current favorites") | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/ | `index.html` |
| Spread Options (every ChatGPT version of every spread) | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/spread-options.html | `spread-options.html` |
| Mockups (quick scene ideas by Ravyn / Trinity) | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/mockups.html | `mockups.html` |
| Favorites data (read by all three pages at load time) | https://mydigitalstudioz.github.io/Harlows-Accidental-Journey/favorites.json | `favorites.json` |

**Three pages, one nav.** Every page links to the other two and highlights the one you're on:
- Showcase: the existing top bar keeps its look; after the section links there's a thin divider, then **Showcase** (current, bold + underlined) · **Spread Options** · **Mockups**. (The older "Title designs" link in that bar is the title-treatments section on the showcase, not the Mockups page.)
- Spread Options and Mockups: a `<nav class="pagenav">` pill row under the header meta; the current page's pill is filled with the page accent (`aria-current="page"`).
- **Page tints** (same layout, small identity accent, art stays the focus): Showcase unchanged (cream, rust accent `#b3541e`). Spread Options = soft warm band (5px `#e3a76f` top border + faint peach header gradient `#fbeedd`), rust accent. Mockups = lavender band (5px `#a58bd6` + header gradient `#ece5f8`), lavender paper `#f8f6fc`, accent `#6d4fa8`.

Repo: `MyDigitalStudioz/Harlows-Accidental-Journey`, published by GitHub Pages from `main`.
When you send someone a link, add a cache-buster: `...spread-options.html?v=<short-sha>`.
To link to one card, add its letter as an anchor: `spread-options.html#S05-G`. Every card has `id="<letter>"`.

## Cards and letters

- Each spread (S01 to S24) is a `<section id="S05">` on `spread-options.html`. Each version is an `<article class="card" id="S05-G" data-letter="S05-G" data-status="..." ...>`.
- **Letters are append-only.** A new version gets the next free letter at the end of its spread (S05-H after S05-G). Never re-letter, reorder, or reuse a letter. People's picks and links depend on them.
- **The `render:` line** under a letter (`<span class="render-id">render: S05-E</span>`) is the name the picture had when it was first made, before it got its page letter. Add it whenever the two differ. Showcase images say `render: showcase pNN`.
- **Images:** export each version as a **1400×700 JPEG** (2:1) into `spread-options/`, named in lower case after the letter (`spread-options/s05-g.jpg`). Point the card's `<img class="thumb">` `src` and `data-render` at it. Leave `data-print` empty.
- **Print is parked.** The print-related bits (`data-print`, the "As rendered / Print-ready" toggle on older cards, the `print md5` facts, desat/print-file notes) stay as they are but dormant. Don't add new print variants or build on them until print is un-parked.
- After adding cards, update the section hint ("N versions, oldest first") and the header total ("163 versions"), and check the card count (see Publish).

## Mockups page (`mockups.html`)

- **Spread Options is ChatGPT only.** Its guide just says: "All pictures here are made with ChatGPT. Quick scene mockups live on the Mockups page." Don't put mockup cards on Spread Options.
- **Mockups are quick scene ideas** made by Ravyn (lavender card, `data-maker="ravyn"`, `#F1EEF8`) or Trinity (mint card, `data-maker="trinity"`, `#EAF6F1`). Each card also carries `<span class="maker-tag">Mockup</span>`, so colour isn't the only signal. Finals are always made with ChatGPT. Likeness is rough by design.
- **Letters:** mockups use their own series per spread: **S07-M1, S07-M2, ...** Append-only, never renumber or reuse. Card markup: `<article class="card" id="S07-M1" data-kind="mockup" data-maker="ravyn" data-letter="S07-M1" data-check="Being checked" data-final="" data-summary="...">`. No `data-status` (mockups don't use the four labels).
- **Image:** keep the mockup's own shape (e.g. 16:9) in `mockups/` (`mockups/s07-m1.jpg`). The thumbnail shows the whole picture with a dashed **2:1 crop guide** (centre line = fold), placed by JS from the image's real shape; the lightbox shows the same guide. Each card has a "Hide/Show crop guide" button.
- **"See the final" slot:** every mockup card has `<p class="final-slot" data-final-slot>`. It reads "not made yet" while `data-final=""`; set `data-final="S07-H"` (a real Spread Options letter) and the slot becomes a link to `spread-options.html#S07-H`.
- **Cap:** 2–3 mockups per spread per round.
- **Checks: layout only** (fold, text sky, page edges), shown with the same check notes: green **Checks passed** or grey **Being checked** (default).
- **Filters:** All, Ravyn, Trinity, Any favorite. Section hint: "N mockup(s) this round (cap 2–3)". The header count is computed from the cards.
- **Likes on mockups** go in `favorites.json` → `mockup_picks` (`{"T":[],"F":[],"R":[],"J":[],"L":[]}`, letters like `S07-M1`). They show as dots on the Mockups page only. **Mockups never feed the showcase**: a liked idea gets made as a ChatGPT final, which then goes on Spread Options with a normal letter.
- The Mockups guide explains: what a mockup is, lavender = Ravyn / mint = Trinity, finals are ChatGPT, the 2–3 cap, layout-only checks, the dashed 2:1 box, dots don't reach the showcase, and the M-letter series.
- **First mockup:** Ravyn's S07 scene test was briefly on the options page; on 2026-10-15 it moved to Mockups as **S07-M1** (image `mockups/s07-m1.jpg`), with no stub left behind. The next real S07 ChatGPT option after F (still reserved for the S07-E redo) takes **S07-G**, no skipped letter.

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
  },
  "showing": {"S01": "S01-I", "S02": "S02-D", "...": "...", "S24": "S24-G"}
}
```

- `showing` is the image each spread shows on the showcase **right now**. It's the tie-break baseline: on a tie, the showcase keeps this image. Spread Options marks those cards "On the showcase."
- **Whoever changes picks also refreshes `showing` for that spread in the same edit.** After editing `picks`, work out the new winner by the rules below (or run the reference script) and put that letter in `showing` for the spread. Then the file and the page agree, and later ties stay put.

- `picks` are **page letters** (as shown on the cards), never render IDs. These are current favorites only, normally one per spread per person. Moving a pick means replacing that spread's letter.
- **Both pages read `favorites.json` at load time.** Editing that one file updates the dots on Spread Options *and* the Current favorites on the showcase. There's no second edit.
- `spread-options.html` also has a baked copy (picks only) (`const FAVORITES = {...}`) used only as an offline fallback. Keep it in sync when convenient (paste the `people` object), but the live JSON wins.
- **Example: "Mom likes S05-G"** → add `"S05-G"` to `people.L.picks` (remove any other S05 letter from Lois's list), set `"showing": {"S05": "S05-G", ...}` in the same edit, commit `favorites.json`, and publish. S05-G gets a rose **L** dot, and because Lois's pick outranks the desks, the showcase switches S05 to S05-G (unless Jon has an S05 pick, or S05-G is Needs a fix).
- Same for Jon: add the letter to `people.J.picks`. Picks are not labels. If Jon says "yes, that's the one," also set that card to **Jon's yes**.

## Showcase rules ("Current favorites" on `index.html`)

One image per spread that has cards on Spread Options, computed in the browser from `favorites.json` plus the card statuses on `spread-options.html` (`pickShowcase()` in `index.html`). For each spread, in order:

1. **Jon's pick** (J dot).
2. **Lois's pick** (L dot).
3. **Most desk dots** (T/F/R). On a tie, keep the image currently showing (`showing` in `favorites.json`). If that isn't among the tied versions, use Trinity's pick among the tied (then Folio's, then Ravyn's).
4. **No picks:** keep the current `showing` image if one exists, otherwise Folio's pick, otherwise skip the spread.

**Only real Spread Options cards count.** `pickShowcase()` only considers `main article.card[data-status]` on `spread-options.html` and drops any `-M<n>` letter; a pick for a letter that isn't a real card there (a mockup like S07-M1, a letter not in use, a typo) is ignored. `mockup_picks` is never read by the showcase.

**Eligibility:** a **Needs a fix** card can never be on the showcase. It's skipped, and the next rule applies. When someone's pick in a spread was skipped for this reason, the showcase shows a small hint under that spread: "a pick was skipped: needs a fix".

Under each image: the pickers' dots and the page letter, linked to `spread-options.html#<letter>`. Tapping the image opens the big viewer with arrows, as before. "Read text" shows only for spreads that have page text in `spreadText`.

The tie-break baseline lives only in `favorites.json` → `showing` (seeded 2026-10-15 with the 24 images showing then). Spread titles live in `SPREAD_TITLES` in `index.html`. The old `spreads/p0N-*.jpg` images stay in the repo; they're the offline fallback if the page data can't be fetched.

A reference copy of the rules in Python is at `/workspace/haj-batch/tmp/showcase_pick.py` on the box (`python3 showcase_pick.py <repo path>` prints the expected pick per spread; use it to refresh `showing`).

## Publish process

1. Start from current `main` and note its sha. Create a branch (`cursor/<short-topic>`). Commit only the files you meant to change.
2. Push the branch, then **fast-forward** `main` to it (e.g. `gh api -X PATCH repos/MyDigitalStudioz/Harlows-Accidental-Journey/git/refs/heads/main -f sha=<sha> -F force=false`). If `main` moved, rebase or redo your change on the new main; don't overwrite.
3. Wait for the Pages build (`gh api repos/.../pages/builds/latest` → `built <sha>`).
4. Fetch the live file with `?v=<short-sha>` and compare its size/SHA-256 with the committed file.
5. Verify in a browser: the card count is unchanged unless you added cards (count `main article.card`; it's 163 as of 2026-10-15, after the S07 mockup moved to Mockups as S07-M1), the Mockups page count (1 as of 2026-10-15), the nav works both ways on all three pages, only the four labels appear, no script errors, and it looks right at 390px wide.
6. Only then share the link, with `?v=<short-sha>`.

## Never

- Never force-push, and never rewrite published history.
- Never touch the `Harlows-v2` branch (or the other `Harlows-v*` branches).
- Never re-letter, reorder, delete or reuse card letters.
- Never put mockups on Spread Options or the showcase; they live on `mockups.html`.
- Never use "Banked", "Provisional", "Approved", "locked" or "final" wording on cards or in `favorites.json`. Desk recommendations aren't a separate word; they fold into **Candidate** (with its check note) or a plain note. Only Jon gives a yes, shown as **Jon's yes**.
- "Farrelli Farms" door lettering on the S08 truck is canon. Never describe it as an error.
- Never use **Needs a fix** for anything but fit (fold, page edge, text band).
- Never put a Needs a fix card on the showcase.
- Never delete the old `spreads/p0N` images.
