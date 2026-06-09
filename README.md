# NOFX Railway Template

One-click Railway deployment for [NOFX](https://github.com/NoFxAiOS/nofx) — an AI trading terminal assistant for US stocks, commodities, forex, and crypto.

[![Deploy on Railway](https://railway.com/button.svg)](https://railway.com/new/template)

## What gets deployed

A single container running:
- **NOFX backend** (Go) on internal port 8081
- **NOFX frontend** (nginx) proxied on Railway's `PORT`

Images are pulled from the official GHCR registry (`ghcr.io/nofxaios/nofx`) and always track `:latest`.

## Environment variables

| Variable | Required | Description |
|---|---|---|
| `JWT_SECRET` | Yes | JWT signing secret (min 32 chars). Generate: `openssl rand -base64 32` |
| `DATA_ENCRYPTION_KEY` | No | AES-256 key (Base64, 32 bytes). Auto-generated if not set. |
| `RSA_PRIVATE_KEY` | No | RSA private key (PEM). Auto-generated if not set. |
| `TRANSPORT_ENCRYPTION` | No | Set `true` for HTTPS deployments (default: `false`) |
| `NOFX_TIMEZONE` | No | Timezone (default: `Asia/Shanghai`) |

### Database (optional — defaults to SQLite)

| Variable | Description |
|---|---|
| `DB_TYPE` | `sqlite` or `postgres` |
| `DB_HOST` | Postgres host |
| `DB_PORT` | Postgres port |
| `DB_USER` | Postgres user |
| `DB_PASSWORD` | Postgres password |
| `DB_NAME` | Postgres database name |

## Persistent storage (required)

NOFX stores its SQLite database at `/app/data/data.db`. Without a volume, **all data is lost on every redeploy**.

After deploying, add a volume in the Railway dashboard:

1. Open your service → **Volumes** tab
2. Click **Add Volume**
3. Set mount path to `/app/data`
4. Redeploy

That's it — your data persists across restarts and redeployments.

## Steps to deploy

1. Click **Deploy on Railway**
2. Set `JWT_SECRET` to a random 32+ character string
3. Deploy — your NOFX instance will be live at the Railway-provided URL
4. Add a Volume mounted at `/app/data` (see above) to persist your data
