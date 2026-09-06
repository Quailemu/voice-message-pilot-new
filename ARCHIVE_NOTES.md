# FamilyUpdates Archive Notes

Archive date: 2026-09-06

Repository: https://github.com/Quailemu/family-updates.git

Archive tag to use for restore: `familyupdates-shelved-2026-09-06`

Previous freeze tag: `familyupdates-working-2026-09-06` at commit `3260efaa78eb5bbd0a16aaace4f808684e3cf762`.

## Purpose

This project was shelved as the existing FamilyUpdates / familyupdates.care application. The archive preserves the source code, documentation, Supabase schema migrations, and deployment/run instructions without preserving secrets or live production data.

## How The App Was Built And Run

The app is a Python Streamlit application.

Runtime:

- Python: `python-3.12.10` from `runtime.txt`
- Dependencies: pinned/ranged in `requirements.txt`
- Main entry point: `app.py`
- Variant wrappers: `family_app.py`, `mobile_app.py`, `office_app.py`, `public_app.py`
- Static public/site files: `site/`

Local install:

```bat
python -m venv .venv
.\.venv\Scripts\activate
python -m pip install -r requirements.txt
```

Local run commands:

```bat
streamlit run app.py
.\run_family.cmd
.\run_care_hub_phone.cmd
.\run_care_hub_office.cmd
```

Local ports:

- Family Hub: `http://localhost:8501`
- Mobile: `http://localhost:8502`
- Family Office: `http://localhost:8503`

Production hosting was recorded as Render, with the target public domain `familyupdates.care`.

## Required Environment Variables

Values are intentionally not recorded in Git.

Variables named by the example configuration:

- `APP_FAMILY_LIVE_REFRESH`
- `APP_INVITATION_ONLY`
- `APP_LIVE_REFRESH`
- `APP_MOBILE_LIVE_REFRESH`
- `APP_OFFICE_LIVE_REFRESH`
- `APP_VARIANT`
- `APP_VARIANT_BY_HOST`
- `AUTH_COOKIE_PERSISTENCE_ENABLED`
- `AUTH_COOKIE_SIGNING_KEY`
- `CANONICAL_PUBLIC_HOST`
- `CANONICAL_PUBLIC_HOST_ALIASES`
- `CARE_HOME_BANNER_OBJECT_PATH`
- `CARE_MOBILE_APP_URL`
- `CARE_MOBILE_MAGIC_LINK_REDIRECT_URL`
- `CARE_OFFICE_APP_URL`
- `CARE_OFFICE_MAGIC_LINK_REDIRECT_URL`
- `DEV_AUTH_BYPASS`
- `DEV_AUTH_BYPASS_AUTH_UID`
- `DEV_AUTH_BYPASS_CARE_HOME_ID`
- `FAMILY_APP_URL`
- `FAMILY_INVITE_REDIRECT_URL`
- `FAMILY_MAGIC_LINK_REDIRECT_URL`
- `FAMILY_OFFICE_SETUP_CODE`
- `FAMILY_RECORD_VIDEO_OBJECT_PATH`
- `FAMILY_SESSION_TIMEOUT_SECONDS`
- `MEDIA_BASE_URL`
- `MEDIA_BUCKET_NAME`
- `MEDIA_TEST_VIDEO_OBJECT_PATH`
- `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY`
- `NEXT_PUBLIC_SUPABASE_URL`
- `OFFICE_MFA_REQUIRED`
- `OPENAI_API_KEY`
- `OPENAI_TRANSCRIPTION_MODEL`
- `PASSWORD_RESET_REDIRECT_URL`
- `PUBLIC_FAMILY_RECORD_VIDEO_URL`
- `PUBLIC_MOBILE_RECORD_VIDEO_URL`
- `PUBLIC_OFFICE_RECORD_VIDEO_URL`
- `PUBLIC_UNIVERSAL_DIAGRAM_VIDEO_URL`
- `SUPABASE_SECRET_KEY`
- `SUPABASE_URL`

Local `.env` is ignored and was not committed.

## Connected Services

Recorded connected services:

- GitHub: source control and audit trail.
- Render: live app runtime hosting.
- Supabase: Auth, Postgres, Storage, and Edge Functions.
- Cloudflare: DNS/domain/media delivery records may be present.
- OpenAI API: optional transcription if configured.
- Postmark: possible transactional email provider if configured.
- Microsoft 365: possible operations/support mailbox.

The service register is preserved at `docs/contracts/registers/external_services_and_subscriptions_register.md`.

## Database, Storage, And Configuration Preservation

Preserved in Git:

- Supabase schema migrations: `supabase/migrations/`
- Supabase local config: `supabase/config.toml`
- Supabase Edge Function source: `supabase/functions/get_audio_signed_url/`
- Minimal seed script: `supabase/seed_minimal_pilot.sql`
- Supabase instructions: `supabase/README.md`
- Streamlit config: `.streamlit/config.toml`
- Example secret/env files: `.env.example`, `.streamlit/secrets.example.toml`

Not preserved in Git:

- Supabase database rows.
- Supabase Auth users.
- Supabase Storage uploaded audio/media objects.
- Render service environment variable values.
- Render logs.
- Cloudflare DNS/account configuration.
- Any provider billing state.

These must be checked and exported separately from the provider dashboards if they are needed later.

## Local Backup Notes

A separate local Git mirror backup should contain repository history, branches, and tags. It does not contain ignored files such as `.env`, `.venv`, caches, provider dashboards, database contents, user accounts, or uploaded files.

Important local-only/excluded items at archive time:

- `.env`: ignored, sensitive, not committed.
- `.venv/`: ignored local dependency install, not committed.
- `__pycache__/`: ignored cache files, not committed.
- Render/Supabase/Cloudflare account state: external, not contained in Git.

## Restore Limitations

Restoring from this repository and archive tag can recover the code and schema files, but not the live hosted service, domain routing, secrets, database data, Auth users, uploaded voice messages, or billing/account settings.

To restore a functional deployment, you would need:

- A Python 3.12 environment.
- Dependencies from `requirements.txt`.
- The archived source/tag.
- Supabase project or restored database/storage/auth data.
- Required environment variables set in the hosting environment.
- Render or another hosting provider configured with equivalent build/start commands and routes.
- DNS records for the chosen domain.
