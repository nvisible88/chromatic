---
paths:
- "index.html"
- "supabase/**"
---

# Supabase Rules

## Current setup

- Project URL: `https://roapaipirbcaefnclxgj.supabase.co`
- Table: `chromatic_leaderboard`
- RLS: enabled
- Policies: anon read (true), anon insert (true)
- Auth: client uses anon key (`eyJ`-prefixed JWT) in standard `Bearer` headers

## Rules

- Never use the service_role key in client code.
- The anon key is public by design — committing it is fine.
- Any insert path must respect RLS. Don't disable RLS to "make it work."
- Don't drop the table or alter its schema without explicit user approval.
- Don't log full response bodies — log status codes only.

## Future Edge Function (v0.2)

- Will validate score ≤ theoretical maximum
- Will rate-limit by IP via `x-forwarded-for`, 1 submission per 5 min
- Will profanity-filter names
- Will lock the table to function-only inserts (revoke anon insert policy)
- When this lands, update the rules above.
