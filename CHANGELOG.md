# Changelog

## 2026-05-25
- Installed the full 1,398-line game from `chromatic.html` into `index.html`
- Wired Supabase URL and legacy anon key into the live game
- Added a downloadable 1080x1350 share card generator for finished results
- Fixed late-game missed-answer flow so the next level advances reliably
- Added a failed-approaches note for the final-level miss bug: the first fix added delayed fallback timers, but the issue still resurfaced because the final-level end-game transition needed explicit try/catch and watchdog forcing
- Confirmed GitHub Pages live response 200 with `CHROMATIC — The Color Perception Test` title

## 2026-05-24
- Initial project scaffold: README, CLAUDE.md, CHANGELOG.md, .gitignore, .env.example
- Renamed chromatic.html → index.html for static hosting
- GitHub repo created and pushed
- GitHub Pages deployment configured
