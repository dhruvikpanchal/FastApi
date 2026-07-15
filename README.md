# Full Stack FastAPI Project

FastAPI backend + React frontend template, configured for **local development** (no Docker).

## Stack

- **Backend:** FastAPI, SQLModel, Pydantic, Alembic, PostgreSQL, JWT auth
- **Frontend:** React, TypeScript, Vite, Tailwind CSS, shadcn/ui, TanStack Query/Router
- **Tooling:** uv (Python), npm (Node), Playwright (optional E2E)

## What you need installed

| Tool | Purpose | You have |
|------|---------|----------|
| [Python 3.14+](https://www.python.org/) | Backend | Yes (3.14) |
| [uv](https://docs.astral.sh/uv/) | Python deps | Yes |
| [Node.js 20+](https://nodejs.org/) | Frontend | Yes (22) |
| [PostgreSQL](https://www.postgresql.org/) | Database | Yes (18, service running) |
| [Git](https://git-scm.com/) | Version control | Yes |

## Quick start

### 1. Configure `.env`

Edit the root `.env` file. At minimum set:

- `SECRET_KEY` — generate with: `python -c "import secrets; print(secrets.token_urlsafe(32))"`
- `FIRST_SUPERUSER_PASSWORD`
- **Database** — either:
  - `POSTGRES_URL` — full Neon / hosted connection string (recommended), **or**
  - `POSTGRES_SERVER` / `POSTGRES_USER` / `POSTGRES_PASSWORD` / `POSTGRES_DB` for local Postgres

For local Postgres only, create the database once:

```sql
CREATE DATABASE app;
```

### 2. Backend

```bash
cd backend
uv sync
uv run bash scripts/prestart.sh
uv run fastapi dev app/main.py
```

- API: http://localhost:8000
- Docs: http://localhost:8000/docs

On Windows PowerShell, if `bash` is unavailable, run:

```powershell
uv run python app/backend_pre_start.py
uv run alembic upgrade head
uv run python app/initial_data.py
uv run fastapi dev app/main.py
```

### 3. Frontend

```bash
cd frontend
npm install
npm run dev
```

- App: http://localhost:5173

### Default login

- Email: value of `FIRST_SUPERUSER` (default `admin@example.com`)
- Password: value of `FIRST_SUPERUSER_PASSWORD`

## Project layout

```
backend/     FastAPI API, models, migrations
frontend/    React + Vite UI
scripts/     Helper scripts (e.g. OpenAPI client generation)
.env         Shared environment config
```

## Useful commands

**Backend tests** (with Postgres and `.env` configured):

```bash
cd backend
uv run pytest
```

**Regenerate frontend API client** (backend must be running):

```bash
bash ./scripts/generate-client.sh
```

Or manually download OpenAPI from http://localhost:8000/api/v1/openapi.json into `frontend/openapi.json`, then:

```bash
cd frontend
npm run generate-client
```

## Notes

- Email features need SMTP settings in `.env`. Without them, password-recovery emails are skipped.
- Docker / Traefik / Compose files were removed from this project for a local-only workflow.
