# Automated Public Procurement Risk & Fraud Detection System (CM2603)

End-to-end data engineering and AI decision-support platform designed to ingest unstructured Sri Lankan public procurement records (`promise.lk`, EPMS, COPE audit reports), standardize them into Open Contracting Data Standard (OCDS 1.1) JSON, detect anomalies without labeled training data, and provide cited audit justifications.

## 4-Tier Modular Architecture
1. **Tier 1 — Data Processing Layer (`pipeline/`):** Headless browser scraping (Playwright), schedule table extraction (`pdfplumber`), fuzzy vendor entity resolution (`RapidFuzz`), and OCDS 1.1 standardization.
2. **Tier 2 — Detection & Risk Layer (`engines/`):** Deterministic procedural red flags (OCP Cardinal), CPV-clustered unsupervised anomaly detection (Isolation Forest), and an inflation-adjusted AI Market Pricing Agent.
3. **Tier 3 — Dashboard & Scoring Layer (`frontend/`):** Unified risk aggregation queue and auditor triage interface operating on an Observe–Orient–Decide–Act (OODA) loop.
4. **Tier 4 — OKF & RAG Explanation Layer (`okf_rag/`):** Open Knowledge Format entity graph paired with vector retrieval (`pgvector`) to generate hallucination-free, cited plain-English explanations and interactive Q&A.

## Why the Frontend Uses a Single-Page Architecture (`frontend/index.html`)
The frontend prototype is intentionally engineered as a zero-dependency Single-Page Application (SPA) using vanilla HTML5, Tailwind CSS, and modular JavaScript within `index.html`:
* **Zero Build-Step Friction:** Eliminates Node/Webpack/React dependency overhead so any teammate or evaluator can open and test the UI immediately in any browser or serve it statically.
* **Unified Client-Side State:** Switching between the *Audit Queue*, *Data Ingestion Pipeline*, *Risk Engine Thresholds*, and the *OKF Audit Assistant* happens instantaneously without page reloads or lost chat/audit context.
* **Clean Backend Decoupling:** All UI panels communicate via standard asynchronous JSON payloads (`fetch`), allowing the Python FastAPI/Flask microservices in Tiers 1, 2, and 4 to plug directly into the frontend endpoints as each sub-team completes its sprint.

## Local Setup
```bash
python -m venv DSGP_env
.\DSGP_env\Scripts\activate
pip install -r requirements.txt
playwright install chromium
