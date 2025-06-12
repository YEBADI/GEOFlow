# GEOFlow

**GEOFlow** is a reproducible workflow for automatically downloading gene expression datasets from [GEO](https://www.ncbi.nlm.nih.gov/geo/), performing basic quality control (QC), and generating publication-ready visualizations using [Nextflow](https://www.nextflow.io/) and R.

This repository supports both command-line and web-based usage, with an optional FastAPI backend to trigger workflows from a browser UI.

---

## 🚀 Features

- 🔎 Fetch any public GEO dataset using its accession (e.g. `GSE12345`)
- 📊 Generate boxplots, PCA, and basic QC reports
- ⚙️ Fully reproducible via Nextflow
- 🌐 FastAPI web service for automated execution

---

## 📁 Directory Structure

```
geo-webapp/
├── main.nf               # Main Nextflow pipeline
├── nextflow.config       # Configurations
├── bin/                  # R scripts for download, QC, plotting
│   ├── download_geo.R
│   ├── qc_report.R
│   └── plot_expression.R
├── backend/              # FastAPI server (optional)
│   └── app.py
├── frontend/             # Web form to trigger workflows
├── runs/                 # Stores per-run outputs
├── Dockerfile            # Backend container (optional)
└── README.md             # This file
```

---

## ⚡ Quickstart (CLI)

```bash
# Run the pipeline with a specific GEO ID
nextflow run main.nf --geo_id GSE12345
```

Or use a params config file:

```bash
nextflow run main.nf -params-file runs/example/params.config
```

---

## 🌐 Web App Usage (Optional)

Start the FastAPI server:

```bash
cd backend
uvicorn app:app --reload
```

Then POST a GEO ID to:

```
POST http://localhost:8000/run_geo
Body: { "geo_id": "GSE12345" }
```

This triggers a run and saves results to `runs/<run_id>/results/`.

---

## 📊 Example Output

- `qc_report.pdf`: boxplots, PCA, basic expression checks
- `expression.csv`: parsed expression matrix
- `meta.csv`: (optional) sample annotations

---

## 📦 Requirements

- R (with `GEOquery`, `ggplot2`, etc.) - see requirements.txt
- Nextflow
- Docker
- Python + FastAPI
