# Patient Observation Tracker — Frontend

[![Pages](https://github.com/isutariy-P532-SPRING2026/patient-observation-tracker-frontend/actions/workflows/pages/pages-build-deployment/badge.svg)](https://github.com/isutariy-P532-SPRING2026/patient-observation-tracker-frontend/actions/workflows/pages/pages-build-deployment)

**Live URL:** https://isutariy-p532-spring2026.github.io/patient-observation-tracker-frontend

**Backend API:** https://patient-observation-tracker-backend-cad5.onrender.com

Plain HTML + CSS + JavaScript single-page application for the Patient Observation Tracker. No frameworks, no build step — runs entirely in the browser and communicates with the Spring Boot backend via fetch API calls.

---

## Pages

| File | Description |
|------|-------------|
| `index.html` | Patient list — view all patients, add a new patient |
| `patient.html?id={n}` | Patient detail — record measurements and category observations, evaluate diagnostic rules, reject observations, view full observation history |
| `catalogue.html` | Catalogue management — create phenomenon types (quantitative/qualitative), add phenomena to qualitative types, add protocols, create diagnostic rules |
| `logs.html` | Logs viewer — command log and audit log side by side |

---

## How to Run Locally

No build step required. Open any HTML file directly in a browser:

```bash
# Option 1 — just open the file
open index.html

# Option 2 — serve with Python (avoids CORS issues)
python3 -m http.server 3000
# then visit http://localhost:3000
```

> **Note:** The frontend fetches data from the Render.com backend by default (configured via `const API_BASE` at the top of each page's `<script>`). To point at a local backend, change the base URL to `http://localhost:8080`.

---

## Key Features

- **Dynamic unit dropdown** — when a staff member selects a quantitative phenomenon type, the unit dropdown is auto-populated from that type's allowed units (fetched from the API, not hardcoded).
- **Dynamic phenomenon dropdown** — selecting a qualitative phenomenon type fetches and populates its phenomenon options.
- **Rule evaluation** — clicking "Evaluate Diagnostic Rules" fires a POST to the backend and shows inferred concepts inline (never auto-saved).
- **Reject observation** — any active observation row has a Reject button that prompts for a reason; the observation stays visible in the table with a REJECTED badge for audit.
- **Observation type badges** — each observation row is visually tagged as Measurement or Category.

---

## Architecture

All pages follow the same pattern:

```
HTML structure (semantic, no framework)
    ↓
Inline <script> with fetch() calls
    ↓
REST API  (https://patient-observation-tracker-backend-cad5.onrender.com/api/...)
```

There is no client-side routing, no state management library, and no bundler. Each page is self-contained.

---

## Deployment

This repository is deployed automatically to **GitHub Pages** from the `main` branch root. Any push to `main` triggers a Pages rebuild.

To deploy your own copy:

1. Fork this repository
2. Go to **Settings → Pages**
3. Set source to `Deploy from a branch` → `main` → `/ (root)`
4. Update the `API_BASE` constant in each HTML file to point to your backend

---

## Related Repository

Backend (Spring Boot): [isutariy-P532-SPRING2026/patient-observation-tracker-backend](https://github.com/isutariy-P532-SPRING2026/patient-observation-tracker-backend)
