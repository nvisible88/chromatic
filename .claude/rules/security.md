---
paths:
- "**/*"
---

# Security Rules

- Never read, log, or output `.env` values.
- Never commit `.env` or `.env.*` files.
- The Supabase anon key in `index.html` is intentionally public — it's safe to commit. The service_role key is not — never paste it, never read it, never log it.
- Never use `git push --force` on main.
- Never use `rm -rf` without explicit user confirmation in the same message.
- For any new external API integration, the key goes in environment-injected config — not hardcoded — unless it's a public-by-design key like the Supabase anon key.
