# Changelog

## v0.1 — MVP shipped (2026-05-25)

### Completed

- 30-level game with HSL-based difficulty curve
- Result screen with three sub-scores and six tier labels
- Supabase leaderboard, end-to-end working
- Top 50 leaderboard with flags
- Share card PNG generator (1080×1350)
- OG + Twitter Card meta tags
- OG image generator tool at `/tools/generate-og.html`
- GitHub Pages deployment
- Level-30 freeze bug fix (watchdog + try/catch in `scheduleLevelAdvance`)

### Failed approaches

- **First deploy was a 64-line placeholder stub.** The full game existed locally but was never copied over. Lesson: always verify file size and content after a "completed" file operation. Don't trust a completion claim without a sanity check.
- **First Supabase URL included a `/rest/v1/` suffix.** The client code prepends that itself — would have caused double-slash 404s. Lesson: bare project URL only.
- **First Supabase key was the new `sb_publishable_` format**, not the legacy JWT anon key. The client code uses standard JWT `Bearer` headers, so the `eyJ`-prefixed key is required.
- **First "fix" for the level-30 freeze didn't actually fix it.** Lesson: never claim a bug is fixed without reproducing the failure condition first.

### Decisions made

- Single HTML file, no build step. Zero deploy friction, ~44KB acceptable.
- HSL color space — perceptually intuitive deltas.
- Three sub-dimensions match the Farnsworth-Munsell test structure.
- Anon key in client code — it's designed to be public, RLS protects writes.
- Pre-game name capture deferred — risk of dropping conversion at the funnel top.

### Known limitations

- No anti-abuse on leaderboard inserts. Anyone can script high scores. Acceptable until v0.2.
- Percentile labels are marketing copy ("Top 4%"), not derived from real data.
- `og.png` not yet generated and committed — meta tag points to a 404.
- No mobile-specific smoke test on iOS Safari yet.

### Next (v0.2 candidates)

- Generate `og.png` and commit it (highest priority — link previews broken until done)
- Verify Copilot freeze-bug fix on the live site by reproducing the trigger condition
- Pre-game name + country capture
- Basic analytics (Plausible or Supabase-derived)
- Mobile smoke test
- Anti-abuse Edge Function (after first ~50 real submissions)
