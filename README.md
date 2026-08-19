# Neural Nexus

**Your AI-powered developer problem solver.**

Neural Nexus is a hackathon-ready developer assistant focused on Git friction, debugging, dependency problems, test failures, and verified fixes. The UI is a React/Vite dashboard and the backend is a FastAPI service with a SQLite activity store.

## Run locally

```powershell
npm install
npm run dev
```

In a second terminal:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r backend/requirements.txt
uvicorn backend.app.main:app --reload --port 8000
```

Open `http://localhost:5173`.

The backend inspects the current workspace by default. Point it at another local repository with `NEURAL_NEXUS_REPOSITORY`. SQLite is the zero-config demo default.

## Safety model

Commands are allowlisted and classified as `safe`, `caution`, or `dangerous`. Unknown commands and destructive Git operations are never executed. Caution and dangerous commands return `confirmation_required` until the caller explicitly confirms them. A fix is only reported as `VERIFIED` after its verification command exits successfully.

## API highlights

- `GET /api/repository`, `/api/git/status`, `/api/git/branches`, `/api/git/log`, `/api/git/diff`
- `POST /api/git/execute`, `/api/git/analyze-error`
- `POST /api/debug/analyze`, `/api/build/analyze`, `/api/dependencies/analyze`, `/api/tests/analyze`
- `POST /api/fix/verify`
- `GET /api/activity`, `/api/metrics`

## Docker

```powershell
docker compose up --build
```

The demo provider is local and deterministic. Add an AI Gateway implementation behind the analysis endpoints when a provider key is available; no key is sent to the frontend.
