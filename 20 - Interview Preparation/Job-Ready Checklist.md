---
title: 30-Point Job-Ready Verification Checklist
aliases:
  - Job-Ready Checklist
---

# 🎯 30-Point Data Engineering Job-Readiness Checklist

To declare yourself job-ready as a production Data Engineer, verify that every checkpoint below is satisfied with concrete evidence from your portfolio and practice drills.

---

## 1. Systems, Linux & Python
- [ ] **CLI Fluency**: Can navigate Linux servers, manipulate files, inspect processes, and handle background daemons purely via CLI.
- [ ] **Bash Scripting**: Writes automated POSIX scripts incorporating strict error handling (`set -euo pipefail`).
- [ ] **Git Operations**: Executes linear rebasing (`git rebase -i`), cleanly resolves merge conflicts, and follows Conventional Commits.
- [ ] **Modern Python**: Writes idiomatic Python 3.12+ code with strict type annotations passing `mypy --strict`.
- [ ] **Data Validation**: Enforces schema contracts on incoming untyped data using Pydantic v2.
- [ ] **Memory Management**: Implements custom generators to stream multi-gigabyte datasets without exceeding RAM bounds (<50MB).
- [ ] **Automated Testing**: Builds modular test suites using pytest fixtures and mocks, maintaining >= 85% test coverage.

## 2. SQL & Relational Databases
- [ ] **Relational Order**: Understands the exact logical execution order of SQL queries and why aliases fail in `WHERE` clauses.
- [ ] **Advanced Windowing**: Constructs complex analytical queries using explicit window frame bounds (`ROWS BETWEEN`).
- [ ] **Hierarchical Queries**: Implements Recursive CTEs to query graph and hierarchical data structures.
- [ ] **Query Performance**: Reads `EXPLAIN (ANALYZE, BUFFERS)` output and optimizes queries using composite and partial B-Tree indexes.
- [ ] **Storage Internals**: Explains the physical storage differences between row-oriented pages (Postgres) and columnar formats (DuckDB/Parquet).

## 3. Data Modeling & Modern ELT
- [ ] **Dimensional Modeling**: Can architect Kimball Star Schemas including Fact tables and Slowly Changing Dimensions (SCD Type 2).
- [ ] **Medallion Architecture**: Can articulate and implement Bronze, Silver, and Gold storage boundaries.
- [ ] **dbt-core Mastery**: Deploys production dbt projects with staging, intermediate, and incremental models utilizing unique keys.
- [ ] **Data Quality Gating**: Enforces schema assertions, generic tests, and custom singular data tests that halt pipeline progression on errors.
- [ ] **Single-Node Analytics**: Utilizes DuckDB and Polars for fast, cost-effective single-node analytical processing.

## 4. Distributed Systems & Streaming
- [ ] **Columnar Formats**: Explains the internal physical structure of Apache Parquet (row groups, dictionary encoding, compression).
- [ ] **Open Table Formats**: Understands Apache Iceberg metadata hierarchies (Catalogs, Snapshots, Manifests) and ACID guarantees.
- [ ] **PySpark Processing**: Writes distributed transformations using the PySpark DataFrame API handling multi-gigabyte datasets.
- [ ] **Spark Optimization**: Diagnoses and resolves shuffle spills, executor OOM errors, and data skew using AQE and key salting.
- [ ] **Orchestration**: Builds and schedules DAGs in Apache Airflow 3.x using the TaskFlow API and `@asset` data-driven scheduling.
- [ ] **Event Streaming**: Explains Kafka partition keys, consumer groups, offset management, and exactly-once semantics.
- [ ] **Kafka KRaft**: Has deployed and configured an Apache Kafka 4.0 cluster running in pure KRaft mode without ZooKeeper.

## 5. Cloud, DevOps & Professional Portfolio
- [ ] **Cloud Primitives**: Understands AWS core data primitives: IAM least-privilege policies, S3 lifecycle rules, Glue, and Athena.
- [ ] **Infrastructure as Code**: Provisions cloud data infrastructure declaratively using modular, state-locked Terraform code.
- [ ] **Containerization**: Writes production multi-stage Dockerfiles and coordinates multi-service environments with Docker Compose.
- [ ] **CI/CD Pipelines**: Builds GitHub Actions workflows automating linting (`ruff`), testing (`pytest`), and deployment.
- [ ] **Observability**: Tracks the 5 pillars of observability (freshness, volume, schema, distribution, lineage) via Soda Core and OpenLineage.
- [ ] **System Design**: Can lead a 45-minute architectural system design session calculating capacity, throughput, and failover mechanics.
- [ ] **Public Portfolio**: Maintains 4+ public, production-grade GitHub repositories with clean code, architectural Mermaid diagrams, and video walkthroughs.
- [ ] **Live Coding Ready**: Solves Medium-level SQL and Python data manipulation problems in real-time under a 30-minute timer.
