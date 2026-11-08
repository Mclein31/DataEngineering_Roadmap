---
id: PRJ-01
name: Project 1: Local Modern ELT Pipeline (Retail Analytics)
aliases:
  - PRJ-01
  - PRJ-01 Spec
  - PRJ-01 README
  - Project 1 - Local Modern ELT Pipeline/README
  - 18 - Projects/Project 1 - Local Modern ELT Pipeline/README
---

# PRJ-01: Local Modern ELT Pipeline (Retail Analytics)

## 📌 Executive Summary
An end-to-end local Modern Data Stack pipeline extracting transactional OLTP retail data from PostgreSQL, landing it into DuckDB columnar storage, and transforming it using `dbt-core` into Kimball dimensional data marts (`fct_orders`, `dim_customers_scd2`, `dim_products`). Visualized via Metabase dashboards.

---

## 🚀 Quickstart & Reproduction Guide (macOS)

### 1. Prerequisites
- macOS Terminal with Homebrew installed
- Docker Engine running (`docker ps`)
- Python 3.12+ and `uv` package manager (`brew install uv`)

### 2. Environment Startup
```bash
# Clone and enter directory
cd ~/Documents/Developer/Personal_Projects/DataEngineering_Roadmap/18\ -\ Projects/Project\ 1\ -\ Local\ Modern\ ELT\ Pipeline

# Start PostgreSQL and Metabase containers
docker compose up -d

# Verify Postgres is healthy and seeded
docker exec -it de-postgres pg_isready -U postgres
```

### 3. Pipeline Execution
```bash
# Initialize uv virtual environment and install dependencies
uv venv .venv
source .venv/bin/activate
uv pip install dbt-core dbt-duckdb dbt-postgres psycopg2-binary duckdb polars pytest

# Run Python delta extractor
python src/extract.py --delta-hours 24

# Execute dbt transformation and test suite
dbt build --project-dir dbt_retail
```

---

## 📂 Repository Structure
```text
project1-modern-elt/
├── dbt_retail/
│   ├── models/
│   │   ├── staging/
│   │   ├── intermediate/
│   │   └── marts/
│   ├── tests/
│   ├── dbt_project.yml
│   └── profiles.yml
├── src/
│   ├── extract.py
│   └── load_duckdb.py
├── docker-compose.yml
├── pyproject.toml
└── README.md
```

---

## 🔗 Project Notes

- [[18 - Projects/Project 1 - Local Modern ELT Pipeline/Architecture|Architecture]]
- [[18 - Projects/Project 1 - Local Modern ELT Pipeline/Verification Checklist|Verification Checklist]]
- Back to [[Project Index]]
