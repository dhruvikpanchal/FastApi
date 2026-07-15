# FastAPI Project - Frontend

Built with Vite, React, TypeScript, TanStack Query/Router, and Tailwind CSS.

## Requirements

- [Node.js](https://nodejs.org/) 20+ (npm)

## Quick start

```bash
npm install
npm run dev
```

Open http://localhost:5173/

Backend URL is set in `.env`:

```env
VITE_API_URL=http://localhost:8000
```

## Generate API client

With the backend running:

1. Download http://localhost:8000/api/v1/openapi.json → `frontend/openapi.json`
2. Run:

```bash
npm run generate-client
```

Or from the repo root (Git Bash / WSL):

```bash
bash ./scripts/generate-client.sh
```

## Code structure

- `src/` — app code
- `src/client/` — generated OpenAPI client
- `src/components/` — UI components
- `src/hooks/` — custom hooks
- `src/routes/` — pages / routes

## End-to-end tests

Start backend and frontend locally, then:

```bash
npx playwright test
npx playwright test --ui
```
