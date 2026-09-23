---
type: project-brain
title: Data Engineering Roadmap — Project Context
project: DataEngineering_Roadmap
status: completed
tags:
  - project
  - data-engineering
  - roadmap
  - obsidian
  - curriculum
  - production
last_updated: 2026-09-23
---

# 🛠️ Data Engineering Master Roadmap — Project Context

## 📌 Overview & Purpose
The **Data Engineering Master Roadmap Obsidian Vault** is a production-grade, 2026-aligned curriculum, operational knowledge hub, and interactive study system designed to take an engineer from foundational software literacy to a job-ready Junior/Mid-level Data Engineer capable of building reliable, distributed, and governed data platforms.

The vault is built strictly in **Vanilla Markdown** for Obsidian, with zero required third-party plugins, zero automation dependencies, and 100% native macOS compatibility (Apple Silicon & Intel). It emphasizes a **free-first, local-first** architecture (using LocalStack, MinIO, DuckDB, Polars, Docker, and Kafka KRaft) to ensure zero accidental cloud billing during student practice.

---

## 🎯 Current Status
- **Vault Status**: `100% Production Ready`
- **Total Markdown Files**: 186
- **Total Curriculum Lessons**: 137 / 137 fully developed
- **Portfolio Capstone Projects**: 5 standalone production architectures with README, Architecture, and Verification Checklists
- **Mermaid Architectural Diagrams**: 14 diagrams (including all 9 core curriculum diagrams)
- **Bidirectional Wikilinks**: 891 links with 100% resolution (0 broken references)
- **Placeholders**: 0 (zero TODO, TBD, or missing sections)

---

## 💻 Technical Foundation & 2026 Modern Paradigm
1. **Modern ELT (dbt + DuckDB) Precedes Distributed Spark**: Single-node processing (DuckDB, Polars) handles sub-terabyte workloads with 90% less infrastructure overhead.
2. **Open Table Formats (Apache Iceberg) Before Distributed Compute**: Understanding metadata trees (snapshots, manifests, manifest lists) makes Spark partition tuning and write modes intuitive.
3. **Kafka KRaft Exclusivity**: Apache Kafka 4.0 removed ZooKeeper; event architectures are taught purely under KRaft metadata consensus.
4. **Airflow 3.x Asset-Centric Scheduling**: Replaces deprecated cron execution dates with event-driven `@asset` data dependencies and the TaskFlow API.
5. **Decoupled Local Infrastructure**: LocalStack and MinIO emulate AWS APIs locally with zero cloud spend.

---

## 📂 Vault Hierarchy (22 Root Directories)
- `00 - Dashboard`: Command Center (`Home.md`), `Daily Log.md`, `Weekly Review.md`, `Skill Matrix.md`
- `01 - Roadmap`: Master Roadmap, 12-Month Plan, Weekly Study System, Phase 1–5 Guides
- `02 - Foundations`: POSIX CLI, Streams, Bash, Git internals (10 lessons)
- `03 - Python`: Python 3.12+, uv, Typing, Pydantic, Polars, Pytest (14 lessons)
- `04 - SQL`: Window functions, CTEs, Execution plans, Indexing (14 lessons)
- `05 - Databases`: OLTP vs OLAP, WAL, MVCC, Pages, B-Trees (6 lessons)
- `06 - Data Modeling`: Kimball Star Schema, 3NF, SCD Types 1–6, Medallion Architecture (8 lessons)
- `07 - Modern ELT & dbt`: DuckDB, dbt-core, Jinja, Schema testing, Incremental models (10 lessons)
- `08 - Data Warehousing`: Snowflake architecture, BigQuery, Clustering, Cost governance (6 lessons)
- `09 - Data Lakes & Lakehouse`: Parquet columnar internals, Apache Iceberg, Delta UniForm, Catalogs (8 lessons)
- `10 - Apache Spark`: Spark 4.0, PySpark, Catalyst optimizer, AQE, Structured Streaming (12 lessons)
- `11 - Airflow & Orchestration`: Airflow 3.x TaskFlow, `@asset` scheduling, Dynamic DAGs (9 lessons)
- `12 - Kafka & Streaming`: Kafka 4.0 KRaft mode, Schema Registry, Exactly-Once Processing (9 lessons)
- `13 - Cloud`: AWS IAM, S3 storage tiers, Athena, Glue Catalog, EMR Serverless (6 lessons)
- `14 - DevOps & Infrastructure`: Multi-stage Docker, Compose, Terraform modular state, GitHub Actions CI/CD (8 lessons)
- `15 - Data Quality & Observability`: Soda Core, Great Expectations, Data Contracts, OpenLineage, Marquez (6 lessons)
- `16 - Data Governance & Security`: RBAC/ABAC, Column masking, Row-level security, KMS encryption, GDPR erasure (5 lessons)
- `17 - System Design`: Capacity math, Idempotency, Lambda vs Kappa, Real-world case studies (6 lessons)
- `18 - Projects`: 5 Capstone specifications, architectural blueprints, and verification checklists (16 files)
- `19 - Certifications`: Study guides for AWS DEA-C01, Databricks Associate, Microsoft Fabric DP-700 (4 files)
- `20 - Interview Preparation`: 50 SQL drills, Python coding bank, Systems defense, STAR stories, Portfolio playbook, 30-point Job-Ready Checklist (7 files)
- `21 - Resources`: Resource Library (RES-01 to RES-23), Software Setup, Books, Documentation, Practice Platforms (5 files)
- `99 - Templates`: Lesson, Project, Weekly, Monthly, and Resource Templates (5 files)
