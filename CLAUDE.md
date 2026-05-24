# CLAUDE — Project Notes for Chromatic

Overview
- Chromatic is a viral, single-page color perception test inspired by the Farnsworth–Munsell 100 Hue Test. The MVP is lightweight, mobile-first, and designed for social sharing.

Architecture
- Single `index.html` file with vanilla JS and CSS; no build step. Optional `config.local.js` (gitignored) for secrets. Leaderboard via Supabase REST API.

File map
- index.html
- README.md
- CLAUDE.md
- CHANGELOG.md
- .gitignore
- .env.example

Key design decisions
- No framework: zero build/deploy friction for GitHub Pages and quick iteration.
- HSL-based color math: perceptually intuitive deltas for hue/saturation/lightness.
- Three sub-dimensions (hue/sat/light) to mirror Farnsworth-Munsell complexity while keeping UI simple.
- Difficulty curve: exponential decay so early levels are approachable and later levels feel expert.

Difficulty curve (MVP)
- 30 levels rotating through hue / saturation / lightness
- Deltas: hue 45°→3°, saturation 40%→2%, lightness 35%→2%
- Grid: 3×3 → 6×6
- Timer: 12s → 5s

Current focus
- Ship MVP to GitHub Pages and get first 100 plays.

Known TODOs / Next priorities
- Add real Supabase credentials via `config.local.js` or environment on deploy (do not commit secrets).
- Percentile labels are marketing copy until we collect a distribution.
- Anti-abuse: add Edge Function + per-IP cooldown for leaderboard inserts.
- Share-card image generation for social sharing.

Live URLs
- GitHub repo: 
- GitHub Pages: 
 - GitHub repo: https://github.com/nvisible88/chromatic
 - GitHub Pages: https://nvisible88.github.io/chromatic/
