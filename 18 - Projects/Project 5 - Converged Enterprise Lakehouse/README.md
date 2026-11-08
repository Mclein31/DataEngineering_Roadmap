---
id: PRJ-05
name: Project 5: Converged Enterprise Lakehouse
aliases:
  - PRJ-05
  - PRJ-05 Spec
  - PRJ-05 README
  - Project 5 - Converged Enterprise Lakehouse/README
  - 18 - Projects/Project 5 - Converged Enterprise Lakehouse/README
---

# PRJ-05: Converged Enterprise Lakehouse & Telemetry Platform

## 📌 Executive Summary
The flagship capstone data platform synthesizing all 5 phases of the curriculum. Ingests dual data streams (daily batch financial transactions and real-time Kafka event telemetry) into **Apache Iceberg** tables on object storage. Orchestrated via **Apache Airflow 3.x** using TaskFlow and event-driven `@asset` data dependencies. Features **dbt-core** dimensional modeling, **OpenLineage** runtime metadata capture into **Marquez**, and column-level PII encryption.

---

## 🚀 Reproduction & Deployment (macOS)
```bash
# Provision infrastructure with Docker Compose and local orchestration
docker compose up -d

# Verify Airflow 3 webserver at http://localhost:8080
# Verify Marquez Lineage UI at http://localhost:3000
# Verify Trino SQL engine at http://localhost:8085

# Execute end-to-end Airflow DAG with asset triggers
airflow dags trigger enterprise_converged_pipeline
```

---

## 🔗 Project Notes

- [[18 - Projects/Project 5 - Converged Enterprise Lakehouse/Architecture|Architecture]]
- [[18 - Projects/Project 5 - Converged Enterprise Lakehouse/Verification Checklist|Verification Checklist]]
- Back to [[Project Index]]
