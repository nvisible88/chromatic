# CHROMATIC — Project Kickoff

You are working on **Chromatic**, a viral color perception test (single-page web app) modeled on the Farnsworth-Munsell 100 Hue Test. The MVP is a single HTML file in this directory as `chromatic.html`. Your job: turn it into a real project, ship it to GitHub Pages, and prepare it for iteration.

## Operating principles

1. **Read `CLAUDE.md` first if it exists.** If it doesn't, create it as part of this kickoff. At the start of every future session, re-read `CLAUDE.md` and the last 5 entries of `CHANGELOG.md` before doing anything else.
2. **Two-file memory system.**
   - `CLAUDE.md` = project state, architecture decisions, conventions, current focus, known TODOs, live URLs. Updated whenever architecture or focus shifts.
   - `CHANGELOG.md` = every meaningful change, dated (YYYY-MM-DD), reverse chronological. Updated at the end of every working session.
3. **Solo developer workflow.** I'm the only contributor. Commit directly to `main`. Conventional commits (`feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `style:`).
4. **Ask before destructive or irreversible actions** — force pushes, history rewrites, deleting branches, dropping Supabase tables, anything touching production data or secrets. Otherwise proceed without permission-checking each step.
5. **No frameworks. No build step.** Vanilla HTML/CSS/JS, single file or minimal splits, deployable as static files. If you want to add tooling, ask first.
6. **Stop and summarize when blocked.** Don't loop on the same error more than twice — surface it to me with what you tried and what you think the cause is.
7. **Never commit real Supabase keys.** Even the anon key — keep it in `index.html` as a placeholder string, and rely on me to swap it in locally OR on a small `config.js` that's gitignored. Decide which approach makes sense and tell me.

## Phase 1 — Repo setup

1. Run `git init` if not already a repo. Set `main` as the default branch (`git branch -M main`).
2. Create `.gitignore`:
```
   .DS_Store
   node_modules/
   .env
   .env.local
   *.log
   .vscode/
   .idea/
   config.local.js
```
3. Create `.env.example` with `SUPABASE_URL=` and `SUPABASE_ANON_KEY=` as documentation only (placeholders).
4. Rename `chromatic.html` → `index.html` so it serves at the site root.
5. Create `README.md` with:
   - One-line description + the Farnsworth-Munsell credibility anchor.
   - Local dev: `python3 -m http.server 8000` then open `http://localhost:8000`.
   - Supabase setup: full SQL block for the `chromatic_leaderboard` table + RLS policies (copy from the comment block at the top of `index.html`).
   - Deployment: brief note that it's deployed via GitHub Pages from `main` branch root.
   - Live URL (filled in once deployed).
6. Create `CLAUDE.md`:
   - **Overview**: what Chromatic is, who it's for, the viral hook.
   - **Architecture**: single HTML file, vanilla JS, Supabase REST API for the leaderboard, no build step.
   - **File map**: `index.html`, `README.md`, `CLAUDE.md`, `CHANGELOG.md`, `.gitignore`, `.env.example`.
   - **Key design decisions**: why no framework (zero deploy friction), why HSL (perceptually intuitive deltas), why three sub-dimensions (hue / saturation / lightness — matches Farnsworth-Munsell structure), why exponential difficulty decay (keeps early levels approachable, makes expert range genuinely hard).
   - **Difficulty curve**: 30 levels rotating through hue/saturation/lightness, deltas 45°→3° / 40%→2% / 35%→2%, grid 3×3 → 6×6, timer 12s → 5s.
   - **Current focus**: ship MVP, get first 100 plays.
   - **Known TODOs / Next priorities**: real Supabase credentials, percentile labels are marketing copy (replace once real distribution exists), anti-abuse on leaderboard insert (Edge Function + per-IP cooldown), share-card image generation for social.
   - **Live URLs**: filled in at the end.
7. Create `CHANGELOG.md` with today's entry:
```markdown
   # Changelog

   ## 2026-05-24
   - Initial project scaffold: README, CLAUDE.md, CHANGELOG.md, .gitignore, .env.example
   - Renamed chromatic.html → index.html for static hosting
   - GitHub repo created and pushed
   - GitHub Pages deployment configured
```
8. Initial commit: `chore: initial project setup`.

## Phase 2 — GitHub

1. Verify `gh` CLI is installed and authenticated (`gh auth status`). If not, tell me the exact commands to run and pause.
2. Create a public repo:
```bash
   gh repo create chromatic --public --source=. --remote=origin \
     --description "A viral color perception test. 30 levels. Farnsworth-Munsell inspired."
```
3. Push `main`: `git push -u origin main`.
4. Report the repo URL back to me.

## Phase 3 — Deploy to GitHub Pages

1. Enable Pages via the gh CLI:
```bash
   gh api -X POST /repos/{owner}/{repo}/pages \
     -f "source[branch]=main" -f "source[path]=/"
```
   If that fails (auth scope, etc.), fall back to instructing me to enable it in the repo settings (Settings → Pages → Source: `main` / root).
2. Site URL will be `https://<your-github-username>.github.io/chromatic/`.
3. **Important**: GitHub Pages caches aggressively. Add a `<meta http-equiv="Cache-Control" content="no-cache, no-store, must-revalidate">` tag in `index.html` `<head>` to make iteration smoother. Also wait ~1–2 minutes after first push before the site appears.
4. Add a custom 404 if it makes sense (skip for MVP, just note as a TODO).
5. Wait for the deployment to go live, then `curl -I` the URL to confirm a 200 response.

## Phase 4 — Final pass

1. Open the live URL and smoke-test: play through 3 full games. Note anything visibly broken (layout, color rendering, timer drift, button states).
2. Confirm the Supabase placeholder strings in `index.html` are clearly marked with the `YOUR_SUPABASE_URL_HERE` / `YOUR_SUPABASE_ANON_KEY_HERE` sentinels.
3. Verify README accurately reflects the setup steps you actually performed.
4. Fill in the live URL and GitHub repo URL in `CLAUDE.md` (under a "Live URLs" section at the top).
5. Final commit: `docs: add live deployment URLs`.
6. Push.

## Deliverables checklist

- [ ] Clean repo: `index.html`, `README.md`, `CLAUDE.md`, `CHANGELOG.md`, `.gitignore`, `.env.example`
- [ ] GitHub repo created and pushed
- [ ] GitHub Pages enabled and live
- [ ] Smoke test passed
- [ ] Both memory files reflect current state, with live URLs in `CLAUDE.md`
- [ ] Three things reported back to me: GitHub repo URL, live Pages URL, and any issues found during smoke test

Start with Phase 1. Confirm each phase complete before moving to the next.