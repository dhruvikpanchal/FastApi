# FastAPI Project - Backend

## Requirements

- [uv](https://docs.astral.sh/uv/)
- PostgreSQL
- Root `.env` configured

## Setup

```console
uv sync
```

Activate the environment if you prefer (optional with `uv run`):

```console
# Windows PowerShell
.venv\Scripts\Activate.ps1
```

Use the interpreter at `backend/.venv/Scripts/python.exe` in your editor.

## Run

From `./backend/`:

```console
uv run python app/backend_pre_start.py
uv run alembic upgrade head
uv run python app/initial_data.py
uv run fastapi dev app/main.py
```

## Workflow

- Models: `./backend/app/models.py`
- API routes: `./backend/app/api/`
- CRUD: `./backend/app/crud.py`

## Tests

```console
uv run pytest
```

Coverage HTML is written to `htmlcov/index.html`.

## Migrations

```console
uv run alembic revision --autogenerate -m "Add column ..."
uv run alembic upgrade head
```

To skip Alembic and auto-create tables, see comments in `./backend/app/core/db.py` and `scripts/prestart.sh`.

## Email templates

Templates live in `./backend/app/email-templates/` (`src` → MJML, `build` → HTML).
Use the [MJML VS Code extension](https://github.com/mjmlio/vscode-mjml) to export HTML into `build/`.
