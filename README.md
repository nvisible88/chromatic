# Chromatic

A viral color perception test inspired by the Farnsworth–Munsell 100 Hue Test.

Local development

Run a simple static server and open the site:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

Supabase setup (example SQL)

```sql
CREATE TABLE chromatic_leaderboard (
  id uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name text NOT NULL,
  score integer NOT NULL,
  time_ms integer NOT NULL,
  played_at timestamptz DEFAULT now(),
  metadata jsonb DEFAULT '{}'
);

ALTER TABLE chromatic_leaderboard ENABLE ROW LEVEL SECURITY;

CREATE POLICY "public_insert" ON chromatic_leaderboard
  FOR INSERT
  USING (true)
  WITH CHECK (
    name IS NOT NULL AND name <> '' AND score >= 0
  );

-- Tighten RLS for production; consider Edge Function to rate-limit
```

Deployment

This project is intended to be deployed to GitHub Pages from the `main` branch root.

Live site: (filled in after deployment)
