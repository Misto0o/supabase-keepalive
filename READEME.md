# Supabase Keepalive

A GitHub Actions workflow that pings my Supabase projects every 6 days to stop them from auto-pausing due to inactivity (free tier pauses after 7 days).

## How it works

`.github/workflows/supabase-keepalive.yml` runs on a schedule (`0 0 */6 * *` — every 6 days) and hits `/auth/v1/health` on each project. This is a lightweight public health-check endpoint — it just confirms the project is alive, no database access needed.

> Note: don't ping `/rest/v1/` (the bare root path) — that endpoint requires the `service_role` key and will 401 even with a valid `anon` key.

Can also be run manually anytime via **Actions → Supabase Keepalive → Run workflow**.

## Projects pinged

| Project | URL |
|---|---|
| MistAI Key System | `cynsmxhjchcjcjivnkte.supabase.co` |
| Digital Taboo | `yiacjatoobjbozopxjvq.supabase.co` |
| HoopPortal | `hpuikheuntquldqdewbr.supabase.co` |

## Required secrets

Set these in **Settings → Secrets and variables → Actions**. Each is the project's `anon` `public` key, found at:
`Supabase Dashboard → [project] → Settings → API Keys → Legacy anon, service_role API keys`

- `SUPABASE_MISTAI_ANON_KEY`
- `SUPABASE_DIGITALTABOO_ANON_KEY`
- `SUPABASE_HOOPPORTAL_ANON_KEY`

## Adding a new project

1. Add a new step to the workflow following the existing pattern (swap in the project URL)
2. Add its `anon` key as a new repo secret
3. Done — no need to touch the actual project's own repo