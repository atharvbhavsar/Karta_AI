# KARTA — AI Credit Intelligence Platform (Backend)

Welcome to the backend infrastructure for **KARTA**, the AI-powered credit intelligence platform crafted for Indian NBFCs. This layer provides 6 robust microservice architectures simulating advanced ML inferences, AI orchestration, and automated pipeline generation designed expressly for the Hackathon Demo.

## Requirements
- **Python 3.11+**
- PostgreSQL (Active models are supported, although the initial configuration runs purely via local SQLite bindings dynamically via SQLAlchemy if DB variables aren't injected).

## Installation

### 1. Configure the Python Environment
We highly recommend isolating dependencies via `venv`:
```bash
python -m venv venv

# On Mac/Linux:
source venv/bin/activate

# On Windows:
venv\\Scripts\\activate
```

### 2. Install Dependencies
```bash
pip install fastapi uvicorn sqlalchemy psycopg2-binary requests
```

---

## Environment Variables
Create a local `.env` and export these mappings to customize production outputs, or rely on the defaults for the demo environment:
- `DATABASE_URL` (Defaults to local `postgresql://...` strings mapped in `config.py`)
- `CLAUDE_API_KEY` (Auth for future LLM integration)
- `AWS_ACCESS_KEY` & `AWS_SECRET_KEY` (S3 bindings for File Uploads)
- `CHROMA_DB_PATH`
- `UPLOAD_FOLDER` (Defaults to local `/uploads`)
- `MAX_FILE_SIZE` (Defaults to `10.0` megabytes)

---

## Running the Server
FastAPI maps automatically via the `uvicorn` engine. Execute the following command from the root directory to go live:
```bash
uvicorn main:app --reload
```
You can access the Swagger UI directly by navigating to `http://localhost:8000/docs`

---

## Resetting Demo Data
This system comes hardcoded with the complete **ABC Manufacturing Ltd** test profile. To ensure smooth, repetitive hackathon demonstrations without DB clustering, use the absolute wipe command:
**Direct GET Request:** `http://localhost:8000/api/demo/reset`

---

## Endpoints Guide

Here map the exact controller URLs functioning locally:

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/health` | Standard AWS/Azure availability ping yielding basic 'ok' parameters. |
| `POST` | `/api/upload` | Orchestrates raw financial Form-Data (.pdf PDFs) triggering DB initializations. |
| `POST` | `/api/analyze/{id}` | The Master Controller. Invokes all 5 ML Services natively chaining OCR -> Fraud -> News RAG -> Scoring -> CAM Document Generation sequentially. |
| `GET` | `/api/status/{id}` | Immediate tracker fetching `percentage_complete` integer polls for React dashboard UIs. |
| `GET` | `/api/results/{id}` | Gathers deep aggregated JSON datasets mapping SHAP algorithms alongside raw Credit Underwriting metrics safely. |
| `GET` | `/api/fraud/{id}` | Retrieves parsed Fake ITC mismatches, NetworkX circular mapping matrices, and MCA regulatory flags. |
| `GET` | `/api/fraud/graph/{id}` | Returns interactive raw HTML scripts rendering PyVis/Vis.js interactive Network Graphs via iframes. |
| `GET` | `/api/ews/{company_id}` | Active Early Warning System tracker detailing 15 variables merging API news signals with internal DB payment structures tracing current month predictions. |
| `POST` | `/api/ews/acknowledge/{id}` | Converts Boolean state for direct RM interface actions resolving specific Warning triggers. |
| `GET` | `/api/ews/all-loans` | Aggregate RM Dashboard querying database row counts fetching exact portfolio volume tracking specific unread alerts mappings safely. |
| `POST` | `/api/cam/generate/{id}` | Simulated .docx compiler engine aggregating all variables explicitly compiling standard Credit Memos. |
| `GET` | `/api/cam/download/{id}` | Fast streaming API serving physically hosted Document bytes manipulating content-disposition mapping. |
| `GET` | `/api/cam/preview/{id}` | Fast pre-loader mapping raw NLP summaries mapping abstract text vectors directly. |
| `GET` | `/api/demo/reset` | Resets the SQLite/PostgreSQL ABC datasets perfectly wiping previous session variables immediately. |
