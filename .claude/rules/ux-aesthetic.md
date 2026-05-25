---
paths:
- "index.html"
- "tools/**"
---

# UX & Aesthetic Rules

## Design system (locked)

| Token        | Value     |
|--------------|-----------|
| Background   | `#0a0a0b` |
| Elevated bg  | `#131316` |
| Card bg      | `#18181c` |
| Ink          | `#f4f0e8` |
| Ink dim      | `#a8a39a` |
| Ink faint    | `#555048` |
| Line         | `#26252a` |
| Line soft    | `#1c1b20` |
| Accent       | `#e8c547` |
| Danger       | `#d9534f` |
| Success      | `#6fbf73` |

## Typography

- **Display copy and headings:** Fraunces — italic for emphasis, weight 300–400
- **Metrics, eyebrows, labels:** JetBrains Mono — uppercase with wide letter-spacing for category labels

## Tone

- Credibility-first. The Farnsworth-Munsell anchor is what separates this from a TikTok quiz — don't write copy that undercuts it.
- No emoji in body copy. Flag emoji in the leaderboard is the only exception.
- Result labels are flattering but never sycophantic. The floor tier ("Functional color vision") still implies competence — never insult the user.
- Italic Fraunces is the "voice" — use it for emphasis the way you'd use a stress accent.

## Layout

- Generous whitespace. The page should feel like a gallery wall, not a dashboard.
- Subtle film grain overlay (already in CSS) stays — it's part of the brand.
- Animations are slow and confident, never bouncy.

## Don't

- Don't add icon libraries (Lucide, Font Awesome, etc.). SVG inline if needed.
- Don't add a sans-serif system font — Fraunces + Mono is the whole stack.
- Don't add gradients beyond what's already in the radial bg subtleties.
- Don't change the gold accent color — it's calibrated against the dark bg.
