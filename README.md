# RICE / ICE Prioritization Tool

A single-page tool for scoring and ranking feature ideas using the RICE and
ICE prioritization frameworks. No backend, no build step, no dependencies —
open `index.html` in a browser and it works.

**[Live demo →](#)** *(add your GitHub Pages link here once published)*

## Why this exists

Roadmap debates default to "whoever argues loudest wins" without a shared,
inspectable way to compare ideas. RICE and ICE don't make the decision for
you, but they force every idea onto the same footing — same inputs, same
formula — so disagreements become about a specific number (is Reach really
3,000? is Confidence really 80%?) instead of vibes.

This tool exists to make that scoring fast enough to actually use in a real
prioritization meeting, instead of a spreadsheet nobody opens after the
first week.

## Features

- **Both frameworks**: switch between RICE (Reach × Impact × Confidence ÷
  Effort) and ICE (average of Impact, Confidence, Ease) — they're different
  tools for different situations, not a strict up-or-downgrade of each other
- **Live ranking**: the list re-sorts by score once you finish editing a
  field (tab/click away, or press Enter) — scores update instantly as you
  type, without the list jumping around mid-keystroke
- **Relative score bars**: RICE scores have no fixed scale — a "960" means
  nothing on its own, only relative to your other features. Each score is
  shown as a filled bar relative to your highest-scoring feature, so
  priority is visible at a glance, not just as a raw number. With only one
  feature in the list, no bar is shown — there's nothing to compare it to
  yet. ICE scores, which are always out of 10, show an absolute bar instead.
- **Reach period matters**: Reach has no fixed unit — pick one period (e.g.
  "per quarter") and use it for every feature in the same list, or scores
  won't be comparable. The tool doesn't enforce this; it's on you to stay
  consistent.
- **Clear first run**: opens empty with the scoring explanation expanded,
  and an explicit "Load an example" button — never silently pre-filled data
  you might mistake for your own
- **No setup, no account, no server**: everything runs client-side; your
  data is saved to your own browser's local storage only
- **Export**: copy the ranked list as a Markdown table (for pasting into
  Notion, Slack, a PRD) or download it as CSV
- **Accessible**: full keyboard support including arrow-key tab switching,
  visible focus states, and screen-reader labels on every field

## How it works

Everything lives in one file, `index.html` — HTML for structure, CSS for the
worksheet-style visual design, and vanilla JavaScript for the scoring logic,
sorting, and local storage. No frameworks, no build step, no npm install.

```
you type into a row → JS recalculates that row's score → list re-sorts →
top-ranked row is highlighted → state saved to localStorage
```

## Running it locally

No installation needed — clone the repo and open the file:

```bash
git clone https://github.com/<your-username>/rice-ice-tool.git
cd rice-ice-tool
open index.html   # macOS; on Windows, just double-click the file
```

## Deploying it publicly

This is a static file, so [GitHub Pages](https://pages.github.com/) is the
natural fit — free, no server, no API key, nothing that can incur cost no
matter how much traffic it gets:

1. Push this repo to GitHub (public)
2. Repo → Settings → Pages → under "Build and deployment," set Source to
   "Deploy from a branch," branch `main`, folder `/ (root)`
3. Save — GitHub gives you a URL like
   `https://<your-username>.github.io/rice-ice-tool/` within a minute or two

## Limitations

- **Data lives only in one browser.** Local storage isn't synced across
  devices or browsers — this is a personal scratchpad tool, not a shared
  team database. Adding real multi-user persistence would mean adding a
  backend, which was a deliberate scope cut to keep this dependency-free.
- **RICE and ICE are opinionated frameworks**, not objective truth. Garbage
  inputs (a wildly optimistic Reach estimate) produce a garbage-but-official-
  looking score. The tool clamps out-of-range and negative values so they
  can't break the math, but it can't and doesn't validate whether your
  estimates are any good — see [Impact-Confidence-Ease vs. RICE](https://www.intercom.com/blog/rice-simple-prioritization-for-product-managers/)
  for context on when each framework fits.
- **No undo** beyond individual row deletion — "Clear all" asks for
  confirmation but is not reversible.

## Possible next steps

- Shareable links (encode state in the URL so you can send a specific
  ranked list to someone without them re-entering data)
- A "weight" setting so teams can tune how much Effort should discount a
  score
- Side-by-side RICE vs. ICE comparison for the same feature list

## Tech stack

HTML, CSS, vanilla JavaScript. No frameworks, no build tools, no
dependencies.

## License

MIT — see [LICENSE](LICENSE).
