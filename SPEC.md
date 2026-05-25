# SPEC — Chromatic

## Project

**Chromatic** is a viral, single-page color perception test.

**Hook:** "Designers and artists see what others miss. 30 levels. Most people fail."

**Credibility anchor:** Farnsworth-Munsell 100 Hue Test — the clinical gold standard used by ophthalmologists, design schools, paint manufacturers, and quality-control labs.

---

## v1 Definition of Done

All items shipped as of 2026-05-25.

- [x] 30 levels rotating through hue / saturation / lightness
- [x] HSL-based difficulty curve — deltas 45°→3° / 40%→2% / 35%→2%
- [x] Grid size 3×3 → 6×6, timer 12s → 5s
- [x] Scoring: base + speed bonus + streak bonus + level multiplier
- [x] Result screen with three sub-scores and six tier labels
- [x] Supabase leaderboard with RLS, anon read + insert
- [x] Top 50 display with name + country flag + score + time
- [x] Share card downloadable PNG (1080×1350)
- [x] OG + Twitter Card meta tags
- [x] GitHub Pages deployment

---

## v1 Explicitly Out of Scope

- Anti-abuse hardening (rate limiting, server-side score validation)
- Real percentiles (current tier labels are marketing copy)
- Share-card auto-post to social platforms
- Account system or persistent identity
- Multiple languages
- Sound or haptics
- Build step of any kind

---

## v2 Candidates (priority order)

1. Generate and commit `og.png` — link previews are broken until this exists
2. Pre-game name + country capture — reduces friction at leaderboard submit
3. Anti-abuse Edge Function — rate limit by IP, profanity filter, score ceiling
4. Real percentile calculation — derived from actual submission distribution
5. Mobile-optimized share card
6. Hungarian translation
