# Development (local, no Docker)

## Prerequisites

- Python 3.14+ and [uv](https://docs.astral.sh/uv/)
- Node.js 20+ and npm
- PostgreSQL running locally
- Root `.env` configured (especially `POSTGRES_*`, `SECRET_KEY`, `FIRST_SUPERUSER*`)

## Backend

```bash
cd backend
uv sync
uv run python app/backend_pre_start.py
uv run alembic upgrade head
uv run python app/initial_data.py
uv run fastapi dev app/main.py
```

- API: http://localhost:8000
- Swagger: http://localhost:8000/docs

## Frontend

```bash
cd frontend
npm install
npm run dev
```

- App: http://localhost:5173
- API base URL: `frontend/.env` → `VITE_API_URL=http://localhost:8000`

## Migrations

After changing models in `backend/app/models.py`:

```bash
cd backend
uv run alembic revision --autogenerate -m "Describe change"
uv run alembic upgrade head
```

## Tests

```bash
cd backend
uv run pytest
```

Frontend E2E (backend + frontend must be running):

```bash
cd frontend
npx playwright test
```
