---
title: Portfolio Projects Master Index
aliases:
  - Project Index
---

# 🏗️ Portfolio Projects Master Index

Building standalone production-grade repositories is the cornerstone of the curriculum. Each project below progressively expands your capabilities—from single-node local ELT to petabyte-scale distributed streaming lakehouses.

---

## 📊 Flagship Portfolio Matrix

| ID | Project Name | Target Month | Primary Tech Stack | Core Architecture | Spec Link |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **PRJ-01** | Local Modern ELT Pipeline | Month 5 | PostgreSQL 16, DuckDB, dbt-core, Metabase, Docker Compose | In-place transformation (dbt) over extracted OLTP delta Parquet into star-schema analytical marts | [[Project 1 - Local Modern ELT Pipeline/README\|PRJ-01 Spec]] |
| **PRJ-02** | Scalable Lakehouse Spark Iceberg | Month 7 | PySpark 4.0, Apache Iceberg, MinIO, Trino, Docker | Medallion Architecture (Bronze -> Silver -> Gold) with ACID merges, schema evolution & time-travel | [[Project 2 - Scalable Lakehouse Spark Iceberg/README\|PRJ-02 Spec]] |
| **PRJ-03** | Real-Time Fleet Streaming | Month 8 | Kafka 4.0 KRaft, PySpark Streaming, TimescaleDB, Grafana | Dual-sink streaming: Fast-path telemetry alerts to TimescaleDB + Cold-path archive to MinIO | [[Project 3 - Real-Time Streaming Ingestion/README\|PRJ-03 Spec]] |
| **PRJ-04** | Production Cloud Platform | Month 10 | AWS (IAM, S3, Glue, Athena), Terraform, GitHub Actions, Soda Core | Fully automated serverless lakehouse provisioned via Terraform IaC with automated CI/CD gating | [[Project 4 - Production Cloud Platform Terraform/README\|PRJ-04 Spec]] |
| **PRJ-05** | Converged Enterprise Lakehouse | Month 11 | Apache Iceberg, Airflow 3.x, Kafka 4.0, PySpark 4.0, dbt, OpenLineage | Unified batch/stream convergence with event-driven `@asset` scheduling & column-level lineage | [[Project 5 - Converged Enterprise Lakehouse/README\|PRJ-05 Spec]] |

---

## 🏆 Project Completion & Defense Protocol
Every project repository must contain:
1. `docker-compose.yml` allowing single-command startup (`docker compose up -d`).
2. Comprehensive unit and data quality test suites (`pytest`, `dbt test`, `soda scan`).
3. High-resolution Mermaid architectural diagram in `README.md`.
4. Documented failure recovery, data contracts, and capacity trade-offs.
