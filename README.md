# CrimeLens AI - Python Backend (FastAPI + SQLite + Pandas)

Welcome to the backend service for **CrimeLens AI**. This service provides a REST API for judicial case exploration, semantic keyword search, dynamic dashboard statistics, and historical crime trend analysis.

> **CRITICAL ETHICAL & BENCHMARK NOTICE**  
> All data records and historical trends provided by this service are **strictly synthetic demonstration benchmarks**. They are generated for interface prototyping, machine learning pipeline evaluation, and UI testing. **Do not use this system as a source for real-world legal proceedings or official crime statistics.**

---

## Architecture Overview

```
CrimeLensAI/
├── backend/                   # Python FastAPI service, database & ML pipelines
│   ├── .venv/                 # Active virtual environment (FastAPI, Pandas, Scikit-Learn)
│   ├── data/                  # Dataset cards & limitation metadata
│   ├── models_registry/       # Serialized models & reproducibility audit store
│   ├── services/              # Forecasting, passage search, jobs & doc extraction
│   ├── database.py            # SQLite connection pooling & schema DDL
│   ├── main.py                # REST API routers & lifespan
│   ├── models.py              # Pydantic v2 data models
│   ├── seed_data.py           # Benchmark database seed script
│   └── test_api.py            # Automated test suite (15 tests passing)
│
├── frontend/                  # ALL Frontend code consolidated here
│   ├── node_modules/          # Frontend npm packages
│   ├── src/                   # React 18 + TypeScript source code
│   │   ├── components/        # Reusable UI components (PassageHighlight, TrustBanner, etc.)
│   │   ├── data/              # Typed mock fallback datasets
│   │   ├── pages/             # All 9 module views (Dashboard, Explorer, Trends, etc.)
│   │   ├── services/          # Resilient API client with failover
│   │   ├── types/             # TypeScript interfaces
│   │   └── App.tsx            # Root component & page router
│   ├── index.html             # HTML entry point
│   ├── package.json           # Frontend dependencies & scripts
│   ├── postcss.config.js      # PostCSS configuration
│   ├── tailwind.config.js     # Tailwind CSS theme definition
│   ├── tsconfig.json          # TypeScript strict configuration
│   └── vite.config.ts         # Vite bundler & reverse proxy config
│
├── scripts/                   # One-command reproducibility suite
│   ├── reproduce.ps1          # PowerShell end-to-end reproducer
│   ├── reproduce.bat          # Windows batch reproducer
│   └── reproduce.sh           # Bash reproducer
│
├── package.json               # Root monorepo proxy scripts (npm run dev / build)
├── PROJECT_CASE_STUDY.md      # Authoritative project case study & portfolio document
├── start.bat                  # 1-Click Frontend launcher (navigates into frontend/)
├── start.ps1                  # PowerShell Frontend launcher
├── start_backend.bat          # 1-Click Backend launcher
└── start_backend.ps1          # PowerShell Backend launcher
```

---

## Prerequisites

- **Python 3.10+** (Tested on Python 3.12)
- **pip** (Python package installer)

To check your Python version, open a terminal and run:
```powershell
python --version
```

---

## Step-by-Step Setup Guide

### 1. Open your Terminal
Navigate to the `CrimeLensAI` workspace directory:
```powershell
cd c:\Users\prach\Desktop\CrimeLensAI
```

### 2. Create the Virtual Environment
Create an isolated environment inside the `backend` folder so global packages are not modified:
```powershell
python -m venv backend\.venv
```
*What this does*: Creates a clean, self-contained Python runtime inside `backend\.venv\`.

### 3. Activate the Virtual Environment

**In PowerShell:**
```powershell
.\backend\.venv\Scripts\Activate.ps1
```
*(If you see an execution policy warning in PowerShell, run `Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass` first).*

**In Command Prompt (cmd.exe):**
```cmd
backend\.venv\Scripts\activate.bat
```

### 4. Install Dependencies
Install all required libraries (FastAPI, Uvicorn, Pandas, NumPy, Pydantic, HTTPX):
```powershell
pip install -r backend\requirements.txt
```
*What this does*: Installs FastAPI (API framework), Uvicorn (ASGI web server), Pandas & NumPy (data modeling & calculations), and Pydantic (data validation).

### 5. Seed the Synthetic Database (Optional)
The database auto-seeds itself on server startup. If you ever want to re-seed or reset it manually, run:
```powershell
python -m backend.seed_data
```

### 6. Run the Automated Test Suite
Verify that all 11 unit and integration tests pass:
```powershell
python -m backend.test_api
```
You should see all tests marked `[PASS]` and `OK`.

### 7. Start the FastAPI Development Server
Start the Uvicorn server with auto-reload:
```powershell
uvicorn backend.main:app --reload --host 127.0.0.1 --port 8000
```
*What this does*: Launches the server at `http://127.0.0.1:8000`. The `--reload` flag automatically reloads the server whenever you edit backend code files.

---

## Quick Start (1-Click Run)

You can also start the server directly without typing commands:

- **PowerShell**: Run `.\backend\start_backend.ps1`
- **Command Prompt**: Double-click `backend\start_backend.bat`

---

## Interactive API Documentation (Swagger & ReDoc)

Once the backend is running, open your web browser:
- **Interactive Swagger UI**: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- **ReDoc Documentation**: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

You can test every endpoint directly inside your browser using Swagger's **"Try it out"** button!

---

## API Endpoints Reference

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/health` | Health check verifying SQLite connectivity and indexed case counts |
| `GET` | `/api/cases` | Paginated case records with multi-dimensional filtering (`category`, `status`, `outcome`, `jurisdiction`) |
| `GET` | `/api/cases/{case_id}` | Retrieve full case dossier by ID with timeline, charges, exhibits, and precedents |
| `GET` | `/api/cases/search` | Search case records by keyword `?q=...` across titles, statutes, summaries, and dockets |
| `POST` | `/api/cases` | Create and validate a new synthetic case record (Pydantic schema validation) |
| `GET` | `/api/dashboard/stats` | Aggregated metrics computed via Pandas & NumPy (conviction rates, median days to resolution, category distribution) |
| `GET` | `/api/trends` | Historical trend time series (2012–2025) with computed growth rates |
| `GET` | `/api/categories` | List of available offence categories and active case counts |

---

## Example Requests

### Health Check:
```powershell
curl http://127.0.0.1:8000/api/health
```

### Search Cases:
```powershell
curl "http://127.0.0.1:8000/api/cases/search?q=ransomware"
```

### Retrieve Dashboard Analytics:
```powershell
curl http://127.0.0.1:8000/api/dashboard/stats
```
