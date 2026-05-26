# CLAUDE — Chromatic

Ship a viral color perception test that makes people share their score.

## Tech stack

Vanilla HTML/CSS/JS · Supabase REST API · GitHub Pages · No build step.

## File map

```
index.html              — the entire game (single file)
SPEC.md                 — product spec and v2 candidates
CHANGELOG.md            — versioned history and failed approaches
.gitignore
.env.example
.claude/
  settings.json         — permissions and model
  rules/
    security.md         — secret handling rules
    supabase.md         — Supabase-specific rules and current config
    ux-aesthetic.md     — design system, typography, tone
  agents/
    debugger.md         — systematic debugging protocol
    security-auditor.md — secret leak and RLS audit protocol
```

## Local dev

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy

```bash
git push origin main   # GitHub Pages auto-deploys
```

## Commit format

Conventional commits. Subject line under 60 chars. Co-author line required:
`Co-Authored-By: Claude Sonnet 4.6 <noreply@anthropic.com>`

## Architecture — modes

Two game modes are defined in the `MODES` constant at the top of the script block:

| Key     | Levels | Delta multiplier | Time multiplier | Min time |
|---------|--------|-----------------|-----------------|----------|
| `adult` | 30     | 1.0×            | 1.0×            | 5 s      |
| `kids`  | 15     | 2.0×            | 2.0×            | 10 s     |

`currentMode` (global) holds the active selection. `freshState()` snapshots `currentMode` into `state.mode` and `state.totalLevels` — all game logic reads from state, not the global. `lbMode` (global) controls which leaderboard tab is shown.

## Code conventions

- **Single-file architecture** — all game code lives in `index.html`. Do not split unless explicitly approved.
- **Vanilla JS only** — no frameworks, no npm, no build tools. Zero dependencies.
- **HSL color space** for all color math. Never convert to RGB for game logic.
- **CSS variables** for all theme tokens — defined at `:root`, never hardcoded inline.
- **JetBrains Mono** for UI metrics, eyebrows, and labels. **Fraunces** for display copy and headings.
- No comments that explain what the code does. Only why, when non-obvious.

## Specialist files

- Supabase work → `.claude/rules/supabase.md`
- Visual or copy changes → `.claude/rules/ux-aesthetic.md`
- Debugging a bug → `.claude/agents/debugger.md`
- Anything touching secrets or credentials → `.claude/agents/security-auditor.md`

## Session continuity

- **Uncommitted changes from a previous task** — if `git status` shows modified files at the start of a new task, surface this immediately: "Uncommitted changes from previous task — review and decide commit/discard before proceeding." Do not start new edits until the user has decided.

## Explicit prohibitions — non-negotiable

- **Never commit the Supabase service_role key.** The anon key is safe to commit — it's public by design. The service_role key is not. Never paste it, never read it, never log it.
- **Never add a build step, framework, or npm dependency** without explicit approval in the same message.
- **Never split `index.html`** into multiple files without explicit approval.
- **Never force push to main.**
- **Never claim a file operation succeeded** without verifying file size or content. Lesson: the first deploy was a 64-line placeholder — the full game existed locally but the write was never verified.
- **Never claim a bug is fixed** without reproducing the failure condition first. Lesson: the first "fix" for the level-30 freeze didn't reproduce the trigger, and the bug remained.
- **Don't change MODES multiplier values** (`deltaMultiplier`, `timeMultiplier`, `minTime`, `totalLevels`) without explicit user approval — they're calibrated.
