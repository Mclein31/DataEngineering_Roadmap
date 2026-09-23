---
title: Data Engineering Skill Matrix
aliases:
  - Skill Matrix
---

# 🧠 Data Engineering Skill Matrix

Use this matrix to audit your operational competence across the 16 core Data Engineering disciplines. Update your rating monthly during the Milestone Gate reviews.

### Proficiency Levels
- **0 - None**: No exposure or theoretical understanding.
- **1 - Novice**: Basic understanding; can follow tutorials and explain high-level syntax.
- **2 - Competent**: Can build functional pipelines independently; understands underlying mechanisms and failure states.
- **3 - Production-Ready**: Can architect resilient, performant systems; debugs low-level crashes, memory leaks, and performance bottlenecks under pressure.

---

## 📊 Skill Evaluation Matrix

| Domain | Target Capability | Current Level (0-3) | Verification Evidence / Project | Last Audited |
| :--- | :--- | :--- | :--- | :--- |
| **macOS CLI & POSIX** | Process signals, permission bitmasks, streaming I/O, `sed`/`awk` one-liners | 1 | Shell exercises in [[LNX-01 - Shell Navigation and Permissions\|LNX-01]]–[[LNX-03 - Text Wrangling with grep sed awk\|LNX-03]] | 2026-09-23 |
| **Bash Automation** | Production scripts with `set -euo pipefail`, error trapping, cron scheduling | 0 | [[LNX-04 - Production Bash Scripting\|LNX-04]], [[LNX-05 - Cron Scheduling and Automation\|LNX-05]] | 2026-09-23 |
| **Git / Version Control** | Linear rebasing (`git rebase -i`), trunk-based flows, conventional commits | 1 | PR workflows in [[GIT-01 - Git Internals and Staging\|GIT-01]]–[[GIT-04 - Semantic Versioning\|GIT-04]] | 2026-09-23 |
| **Modern Python (3.12+)** | `uv`, static typing (`mypy --strict`), Pydantic v2 validation, protocols | 1 | Custom ingestion CLI in [[PY-01 - Python Internals and uv\|PY-01]]–[[PY-08 - Context Managers\|PY-08]] | 2026-09-23 |
| **Single-Node Analytics** | Polars LazyFrame expressions, PyArrow serialization, zero-copy Arrow memory | 0 | [[PY-11 - Vectorized Processing with Polars\|PY-11]], [[PY-12 - Columnar Serialization with PyArrow\|PY-12]] | 2026-09-23 |
| **Analytical SQL** | Window frames (`ROWS BETWEEN`), recursive CTEs, grouping sets, anti-joins | 1 | 50 SQL drills, [[SQL-01 - Relational Execution Order\|SQL-01]]–[[SQL-10 - Pivot and Conditional Aggregation\|SQL-10]] | 2026-09-23 |
| **Query Optimization** | Reading `EXPLAIN ANALYZE`, composite B-Tree indexes, join algorithm selection | 0 | Benchmarks in [[SQL-11 - Execution Plans with EXPLAIN\|SQL-11]]–[[SQL-14 - Indexing Strategies and B-Trees\|SQL-14]] | 2026-09-23 |
| **Storage Internals** | Row vs columnar pages, WAL mechanics, MVCC transaction isolation levels | 0 | [[DB-01 - Row vs Columnar Storage\|DB-01]]–[[DB-06 - Analytical Engines ClickHouse and DuckDB\|DB-06]] | 2026-09-23 |
| **Data Modeling** | Kimball Star Schema, SCD Type 1–3, Medallion storage tiers, Data Vault basics | 0 | [[MOD-01 - Relational Normalization 1NF to 3NF\|MOD-01]]–[[MOD-08 - One Big Table vs Star Schema\|MOD-08]], [[Project 1 - Local Modern ELT Pipeline/README\|PRJ-01]] | 2026-09-23 |
| **In-Warehouse ELT (dbt)** | `dbt-core`, incremental models, schema assertions, dynamic Jinja macros | 0 | [[DBT-01 - Modern ELT Architecture\|DBT-01]]–[[DBT-10 - dbt Documentation and Lineage\|DBT-10]], [[Project 1 - Local Modern ELT Pipeline/README\|PRJ-01]] | 2026-09-23 |
| **Data Lakes & Iceberg** | Open table formats, Iceberg metadata trees, ACID on S3, hidden partitioning | 0 | [[LAK-01 - Object Storage Architecture\|LAK-01]]–[[LAK-08 - Open Table Catalogs\|LAK-08]], [[Project 2 - Scalable Lakehouse Spark Iceberg/README\|PRJ-02]] | 2026-09-23 |
| **Distributed Compute** | PySpark 4.0, Catalyst optimization, shuffle tuning, AQE, skew mitigation | 0 | [[SPK-01 - Spark 4 Cluster Architecture\|SPK-01]]–[[SPK-12 - Spark Structured Streaming\|SPK-12]], [[Project 2 - Scalable Lakehouse Spark Iceberg/README\|PRJ-02]] | 2026-09-23 |
| **Orchestration** | Airflow 3.x TaskFlow API, event-driven `@asset` dependencies, dynamic DAGs | 0 | [[AIR-01 - Orchestration Principles\|AIR-01]]–[[AIR-09 - Dagster Asset Alternative\|AIR-09]], [[Project 5 - Converged Enterprise Lakehouse/README\|PRJ-05]] | 2026-09-23 |
| **Real-Time Streaming** | Kafka 4.0 KRaft mode, schema registry (Avro), consumer lag, watermarking | 0 | [[KFK-01 - Event-Driven Fundamentals\|KFK-01]]–[[KFK-09 - Stream Processing Patterns\|KFK-09]], [[Project 3 - Real-Time Streaming Ingestion/README\|PRJ-03]] | 2026-09-23 |
| **Cloud (AWS)** | IAM least-privilege, S3 lifecycle, Athena serverless, Glue Data Catalog | 0 | [[CLD-01 - AWS IAM Security\|CLD-01]]–[[CLD-06 - Cloud Cost Optimization\|CLD-06]], [[AWS Certified Data Engineer DEA-C01\|DEA-C01]] | 2026-09-23 |
| **DevOps & IaC** | Multi-stage Dockerfiles, Docker Compose, Terraform state/modules, GitHub Actions | 0 | [[OPS-01 - Docker Fundamentals\|OPS-01]]–[[OPS-08 - Automated Testing in CI\|OPS-08]], [[Project 4 - Production Cloud Platform Terraform/README\|PRJ-04]] | 2026-09-23 |
| **Reliability & Lineage** | Soda Core data contracts, Great Expectations, OpenLineage, Marquez UI | 0 | [[DAT-01 - The 5 Pillars of Observability\|DAT-01]]–[[DAT-06 - Anomaly Detection and Alerting\|DAT-06]], [[Project 5 - Converged Enterprise Lakehouse/README\|PRJ-05]] | 2026-09-23 |
| **System Design** | Capacity math, backpressure, idempotency, Kappa architecture, failover | 0 | [[DES-01 - System Design Interview Framework\|DES-01]]–[[DES-06 - Case Study IoT Telemetry Engine\|DES-06]] | 2026-09-23 |
