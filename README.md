# my-portal-keepalive

Public GitHub Actions cron that keeps a free Render web service from sleeping after 15 minutes of idle time.

This repository holds **no personal data, no credentials, and no secrets**. The only committed value is the public health-check URL of the web service.

## What it does

- Every 10 minutes, and on demand (`workflow_dispatch`): `GET https://my-portal-pzgj.onrender.com/healthz` with retries, so the free web instance stays warm.
- Every 6 hours (at 00:30, 06:30, 12:30, and 18:30 UTC), and on demand: `POST /internal/sync` with a bearer token stored in the repo's Actions secrets (`SYNC_TOKEN`). The web app itself decides whether a campus sync is needed (older than 6 hours) and will not retry a failed university login.

The application source lives in a separate private repository. This repo is only the pinger.
