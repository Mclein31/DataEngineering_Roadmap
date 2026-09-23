---
title: 12-Month Detailed Master Plan
aliases:
  - 12 Month Plan
---

# 📅 12-Month Detailed Master Plan

Designed for 10–15 hours/week (1–2 hrs/day weekdays, 3–4 hrs on Saturday deep work, 1.5 hrs on Sunday retro) on macOS.

---

## 🗓️ Month 1: Systems Foundations (macOS POSIX CLI & Git)

- **Primary Objective**: Master Unix CLI navigation, shell text wrangling, automated Bash scripts, and Git linear rebasing.
- **Assigned Lessons**:
  - [[LNX-01 - Shell Navigation and Permissions]]
  - [[LNX-02 - Standard Streams and Pipelines]]
  - [[LNX-03 - Text Wrangling with grep sed awk]]
  - [[LNX-04 - Production Bash Scripting]]
  - [[LNX-05 - Cron Scheduling and Automation]]
  - [[LNX-06 - Networking Fundamentals for DE]]
  - [[GIT-01 - Git Internals and Staging]]
  - [[GIT-02 - Branching Strategies for Data]]
  - [[GIT-03 - Conflict Resolution and Rebasing]]
  - [[GIT-04 - Semantic Versioning]]
- **Skills Mastered**: POSIX navigation, stream redirection, sed/awk parsing, Bash scripting with `set -euo pipefail`, Git rebasing, SemVer.
- **Practice Drills**: Complete 15 terminal exercises on Linux Journey; write 3 automated Bash data-moving scripts.
- **Portfolio Project Work**: Scaffold foundational GitHub workspace repository with pre-commit hooks and standard folder structure.
- **Certification Work**: None (focus strictly on systems foundations).
- **Monthly Milestone**: **Milestone Gate 1A**: Pass timed CLI navigation test and execute a Bash log-parser script.
- **Month Review Template**:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 2*: [ ]

---

## 🗓️ Month 2: Production Python & Software Engineering Mechanics

- **Primary Objective**: Transition from scripting to writing robust, typed, object-oriented Python 3.12+ code.
- **Assigned Lessons**:
  - [[PY-01 - Python Internals and uv]]
  - [[PY-02 - Strict Type Hinting and mypy]]
  - [[PY-03 - Data Validation with Pydantic]]
  - [[PY-04 - Functional Mechanics and Itertools]]
  - [[PY-05 - Memory Optimization with Generators]]
  - [[PY-06 - Advanced OOP and Protocols]]
  - [[PY-07 - Metaprogramming with Decorators]]
  - [[PY-08 - Context Managers]]
- **Skills Mastered**: `uv` package management, Python 3.12+ runtime, static typing (`mypy --strict`), Pydantic v2 schemas, memory-efficient generators, OOP protocols, custom decorators, transactional context managers.
- **Practice Drills**: Implement a streaming file reader that processes a 2GB file in <50MB of RAM using generators and Pydantic validation.
- **Portfolio Project Work**: Build a custom Python ingestion utility module packaged via `pyproject.toml`.
- **Certification Work**: None.
- **Monthly Milestone**: Deliver unit-tested custom Python package passing `mypy --strict`.
- **Month Review Template**:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 3*: [ ]

---

## 🗓️ Month 3: Fast In-Memory Processing & Core SQL Querying

- **Primary Objective**: Master fast in-memory data wrangling with Polars/PyArrow and write foundational analytical SQL queries.
- **Assigned Lessons**:
  - [[PY-09 - Structured Logging]]
  - [[PY-10 - Resilient HTTP Ingestion with httpx]]
  - [[PY-11 - Vectorized Processing with Polars]]
  - [[PY-12 - Columnar Serialization with PyArrow]]
  - [[PY-13 - Unit Testing with pytest]]
  - [[PY-14 - Python Packaging with pyproject]]
  - [[SQL-01 - Relational Execution Order]]
  - [[SQL-02 - Filtering and Three-Valued Logic]]
  - [[SQL-03 - Relational Joins and Anti-Joins]]
  - [[SQL-04 - Advanced Grouping Sets and Rollups]]
  - [[SQL-05 - Subqueries and CTEs]]
  - [[SQL-06 - Recursive CTEs]]
- **Skills Mastered**: Structured logging (`structlog`), resilient API ingestion (`httpx`), Polars DataFrames/LazyFrames, PyArrow, pytest with fixtures/mocks, SQL logical execution order, joins/anti-joins, recursive CTEs.
- **Practice Drills**: Complete 20 SQL query drills on Select Star SQL; write comprehensive pytest test suites for Python extractors.
- **Portfolio Project Work**: Standalone Python CLI Tool fetching open API data, validating schemas with Pydantic, and saving Parquet.
- **Certification Work**: None.
- **Monthly Milestone**: **Milestone Gate 1 Exit**: Pass timed 60-minute SQL test on joins/CTEs and deliver tested Python CLI tool.
- **Month Review Template**:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 4*: [ ]

---

## 🗓️ Month 4: Window Functions, Execution Plans & Database Internals

- **Primary Objective**: Master analytical window SQL functions, query execution plan diagnostics, and relational storage internals.
- **Assigned Lessons**:
  - [[SQL-07 - Window Functions Ranking]]
  - [[SQL-08 - Window Functions Value Navigation]]
  - [[SQL-09 - Window Functions Frame Specifications]]
  - [[SQL-10 - Pivot and Conditional Aggregation]]
  - [[SQL-11 - Execution Plans with EXPLAIN]]
  - [[SQL-12 - Relational Access Methods]]
  - [[SQL-13 - Join Algorithms]]
  - [[SQL-14 - Indexing Strategies and B-Trees]]
  - [[DB-01 - Row vs Columnar Storage]]
  - [[DB-02 - Write-Ahead Logging and Durability]]
  - [[DB-03 - MVCC and Isolation Levels]]
  - [[DB-04 - PostgreSQL Vacuum and Bloat]]
  - [[DB-05 - Specialized PostgreSQL Indexes]]
  - [[DB-06 - Analytical Engines ClickHouse and DuckDB]]
- **Skills Mastered**: Window frames (`ROWS BETWEEN`), `EXPLAIN (ANALYZE, BUFFERS)`, composite/partial B-Trees, VACUUM, MVCC, OLTP vs OLAP page storage, DuckDB vectorization.
- **Practice Drills**: Complete 25 LeetCode SQL Medium problems; diagnose and optimize 5 slow execution plans in PostgreSQL.
- **Portfolio Project Work**: Initialize local PostgreSQL and DuckDB instances via Docker Compose for analytics benchmarking.
- **Certification Work**: None.
- **Monthly Milestone**: Optimize an unindexed query on a 5M row PostgreSQL table, reducing runtime by >80%.
- **Month Review Template**:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 5*: [ ]

---

## 🗓️ Month 5: Dimensional Modeling & Modern In-Warehouse ELT (dbt)

- **Primary Objective**: Architect analytical data models and build automated in-warehouse transformation pipelines.
- **Assigned Lessons**:
  - [[MOD-01 - Relational Normalization 1NF to 3NF]]
  - [[MOD-02 - Kimball Dimensional Modeling]]
  - [[MOD-03 - Fact Table Architecture]]
  - [[MOD-04 - Dimension Table Architecture]]
  - [[MOD-05 - Slowly Changing Dimensions]]
  - [[MOD-06 - Medallion Architecture]]
  - [[MOD-07 - Data Vault 2 Basics]]
  - [[MOD-08 - One Big Table vs Star Schema]]
  - [[DBT-01 - Modern ELT Architecture]]
  - [[DBT-02 - Embedded Analytics with DuckDB]]
  - [[DBT-03 - dbt Core Setup and Architecture]]
  - [[DBT-04 - dbt Modeling Layers]]
  - [[DBT-05 - dbt Materializations]]
  - [[DBT-06 - dbt Incremental Models]]
  - [[DBT-07 - dbt Testing Framework]]
  - [[DBT-08 - Advanced Testing and Expectations]]
  - [[DBT-09 - dbt Jinja and Dynamic Macros]]
  - [[DBT-10 - dbt Documentation and Lineage]]
  - [[DW-01 - Cloud Warehouse Architecture]]
  - [[DW-02 - Snowflake Architecture]]
  - [[DW-03 - Snowflake Time Travel and Cloning]]
  - [[DW-04 - Google BigQuery Architecture]]
  - [[DW-05 - Partitioning and Clustering]]
  - [[DW-06 - Warehouse Cost Governance]]
- **Skills Mastered**: 3NF normalization, Kimball Star Schema, SCD Type 2, Medallion storage tiers, `dbt-core`, incremental models, generic and singular tests, Jinja macros, Snowflake/BigQuery architectures.
- **Practice Drills**: Complete dbt Fundamentals tutorials; design dimensional star schemas for e-commerce and SaaS billing.
- **Portfolio Project Work**: **Deliver [[Project 1 - Local Modern ELT Pipeline/README|Project 1: Local Modern ELT Pipeline]] (PostgreSQL + DuckDB + dbt-core + Metabase)**.
- **Certification Work**: Begin reviewing AWS Certified Data Engineer Associate (DEA-C01) exam guide.
- **Monthly Milestone**: **Milestone Gate 2 Exit**: Deliver Project 1 repository with passing dbt build assertions.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 6*: [ ]

---

## 🗓️ Month 6: Modern Data Lakes & Open Table Formats (Apache Iceberg)

- **Primary Objective**: Understand modern Data Lakes and master Open Table Formats (Apache Iceberg).
- **Assigned Lessons**:
  - [[LAK-01 - Object Storage Architecture]]
  - [[LAK-02 - Apache Parquet Internals]]
  - [[LAK-03 - Limitations of Traditional Lakes]]
  - [[LAK-04 - Open Table Format Paradigm]]
  - [[LAK-05 - Apache Iceberg Architecture]]
  - [[LAK-06 - Iceberg Hidden Partitioning]]
  - [[LAK-07 - Delta Lake and UniForm]]
  - [[LAK-08 - Open Table Catalogs]]
- **Skills Mastered**: Object storage mechanics, Apache Parquet internal structure (row groups, dictionary encoding), Iceberg metadata trees (manifests, snapshot isolation), hidden partitioning, schema evolution.
- **Practice Drills**: Inspect raw Parquet metadata using `pyarrow.parquet.read_metadata`; deploy local MinIO and Iceberg REST catalog via Docker.
- **Portfolio Project Work**: Scaffold Project 2 infrastructure (MinIO + Iceberg catalog + Docker Compose).
- **Certification Work**: Review AWS S3, IAM, and Athena documentation for DEA-C01.
- **Monthly Milestone**: Successfully commit ACID transactions to an Iceberg table on MinIO and execute a time-travel rollback query.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 7*: [ ]

---

## 🗓️ Month 7: Distributed Compute with Apache Spark 4.0

- **Primary Objective**: Master distributed compute mechanics using Apache Spark 4.0 and PySpark.
- **Assigned Lessons**:
  - [[SPK-01 - Spark 4 Cluster Architecture]]
  - [[SPK-02 - Spark Connect Architecture]]
  - [[SPK-03 - PySpark DataFrame Mechanics]]
  - [[SPK-04 - Catalyst Optimizer Deep Dive]]
  - [[SPK-05 - Spark SQL Internals]]
  - [[SPK-06 - Shuffling Mechanics]]
  - [[SPK-07 - Join Strategies in Spark]]
  - [[SPK-08 - Adaptive Query Execution]]
  - [[SPK-09 - Spark Unified Memory Management]]
  - [[SPK-10 - Diagnosing Spark OOM and Spills]]
  - [[SPK-11 - Data Skew Mitigation]]
- **Skills Mastered**: Spark cluster architecture, Spark Connect, PySpark DataFrame API, Catalyst Optimizer physical planning, shuffle tuning, AQE, skew mitigation via key salting.
- **Practice Drills**: Run PySpark jobs on multi-gigabyte datasets; inspect Spark UI to locate shuffle stages and executor spills.
- **Portfolio Project Work**: **Deliver [[Project 2 - Scalable Lakehouse Spark Iceberg/README|Project 2: Scalable Lakehouse with PySpark & Apache Iceberg]]**.
- **Certification Work**: Databricks Certified Data Engineer Associate preparation review.
- **Monthly Milestone**: Successfully eliminate data skew in a 10M row PySpark join using key salting.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 8*: [ ]

---

## 🗓️ Month 8: Workflow Orchestration (Airflow 3.x) & Real-Time Streaming (Kafka 4.0 KRaft)

- **Primary Objective**: Automate asset pipelines with Airflow 3.x and stream real-time events with Kafka 4.0 KRaft.
- **Assigned Lessons**:
  - [[AIR-01 - Orchestration Principles]]
  - [[AIR-02 - Airflow 3 Architecture]]
  - [[AIR-03 - TaskFlow API and Dynamic DAGs]]
  - [[AIR-04 - Data-Aware Asset Scheduling]]
  - [[AIR-05 - Event-Driven Orchestration]]
  - [[AIR-06 - Connections and Secrets]]
  - [[AIR-07 - Resilient DAGs and Retries]]
  - [[AIR-08 - Distributed Executors]]
  - [[AIR-09 - Dagster Asset Alternative]]
  - [[KFK-01 - Event-Driven Fundamentals]]
  - [[KFK-02 - Kafka 4 KRaft Consensus]]
  - [[KFK-03 - Broker Internals and Log Partitions]]
  - [[KFK-04 - Producer Mechanics and Idempotence]]
  - [[KFK-05 - Consumer Groups and Offsets]]
  - [[KFK-06 - Delivery Guarantees]]
  - [[KFK-07 - Schema Registry and Avro]]
  - [[KFK-08 - Change Data Capture Debezium]]
  - [[KFK-09 - Stream Processing Patterns]]
  - [[SPK-12 - Spark Structured Streaming]]
- **Skills Mastered**: Airflow TaskFlow API, `@asset` data-driven scheduling, Kafka KRaft consensus, topic partitioning, consumer group lag, Spark Structured Streaming with watermarking.
- **Practice Drills**: Build an Airflow DAG with dynamic asset scheduling; produce and consume 50,000 Avro messages in Kafka.
- **Portfolio Project Work**: **Deliver [[Project 3 - Real-Time Streaming Ingestion/README|Project 3: Real-Time Fleet Streaming & Telemetry Pipeline]]**.
- **Certification Work**: None (Heavy project implementation month).
- **Monthly Milestone**: **Milestone Gate 3 Exit**: Real-time streaming pipeline processing events with sub-5-second latency to Grafana.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 9*: [ ]

---

## 🗓️ Month 9: Declarative Cloud Infrastructure (AWS & Terraform)

- **Primary Objective**: Provision cloud data infrastructure declaratively using Terraform on AWS (and LocalStack).
- **Assigned Lessons**:
  - [[CLD-01 - AWS IAM Security]]
  - [[CLD-02 - Amazon S3 Storage Architecture]]
  - [[CLD-03 - Amazon Athena and Glue Catalog]]
  - [[CLD-04 - Amazon EMR Serverless Spark]]
  - [[CLD-05 - Serverless Compute and VPCs]]
  - [[CLD-06 - Cloud Cost Optimization]]
  - [[OPS-04 - Terraform Syntax and State]]
  - [[OPS-05 - Terraform Modular Architecture]]
  - [[OPS-06 - Remote State and Backend Locking]]
- **Skills Mastered**: AWS IAM least-privilege, S3 storage tiers, Glue Data Catalog, Athena serverless querying, Terraform state locking (S3/DynamoDB) and reusable modules.
- **Practice Drills**: Provision S3 buckets, IAM roles, and Athena workgroups purely via `terraform apply` in LocalStack or AWS sandbox.
- **Portfolio Project Work**: Scaffold Project 4 (Terraform infrastructure modules for AWS data platform).
- **Certification Work**: Intensive study for AWS Certified Data Engineer - Associate (DEA-C01).
- **Monthly Milestone**: Pass full Terraform infrastructure test creating and destroying cloud data resources cleanly.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 10*: [ ]

---

## 🗓️ Month 10: CI/CD Automation, Data Reliability & Governance

- **Primary Objective**: Implement CI/CD automation, pipeline data quality gating, and observability.
- **Assigned Lessons**:
  - [[OPS-01 - Docker Fundamentals]]
  - [[OPS-02 - Multi-Stage Dockerfiles]]
  - [[OPS-03 - Docker Compose Platforms]]
  - [[OPS-07 - GitHub Actions CI-CD]]
  - [[OPS-08 - Automated Testing in CI]]
  - [[DAT-01 - The 5 Pillars of Observability]]
  - [[DAT-02 - Pipeline Testing with Soda Core]]
  - [[DAT-03 - Validation with Great Expectations]]
  - [[DAT-04 - Data Contracts]]
  - [[DAT-05 - OpenLineage and Marquez]]
  - [[DAT-06 - Anomaly Detection and Alerting]]
  - [[GOV-01 - Access Control Models RBAC ABAC]]
  - [[GOV-02 - Column Masking and Row-Level Security]]
  - [[GOV-03 - Data Encryption at Rest and Transit]]
  - [[GOV-04 - Enterprise Governance Unity and Polaris]]
  - [[GOV-05 - Compliance Engineering and GDPR]]
- **Skills Mastered**: Multi-stage Docker optimization, GitHub Actions CI/CD workflows, Soda Core contracts, Great Expectations, OpenLineage metadata capture, RBAC/ABAC, column-level PII masking.
- **Practice Drills**: Configure a GitHub Actions workflow that runs Ruff, Pytest, and blocks PR merges upon test failure.
- **Portfolio Project Work**: **Deliver [[Project 4 - Production Cloud Platform Terraform/README|Project 4: Production Cloud Data Platform]]**.
- **Certification Work**: **Sit and pass the [[AWS Certified Data Engineer DEA-C01|AWS Certified Data Engineer - Associate (DEA-C01)]] exam**.
- **Monthly Milestone**: **Milestone Gate 4 Exit**: Deliver Project 4 repository; earn AWS DEA-C01 certification.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 11*: [ ]

---

## 🗓️ Month 11: Distributed System Design & Converged Enterprise Capstone

- **Primary Objective**: Master distributed system design and engineer the final Converged Enterprise Capstone.
- **Assigned Lessons**:
  - [[DES-01 - System Design Interview Framework]]
  - [[DES-02 - Pipeline Idempotency and Backfills]]
  - [[DES-03 - Architecture Patterns Batch vs Stream]]
  - [[DES-04 - Case Study Clickstream Analytics]]
  - [[DES-05 - Case Study Financial Ledger]]
  - [[DES-06 - Case Study IoT Telemetry Engine]]
- **Skills Mastered**: High-throughput pipeline design, capacity math (MB/s to storage/yr), backpressure handling, idempotency, converged lakehouse architectures.
- **Practice Drills**: Solve 3 comprehensive system design case studies on a virtual whiteboard.
- **Portfolio Project Work**: **Deliver [[Project 5 - Converged Enterprise Lakehouse/README|Project 5: Converged Enterprise Lakehouse & Telemetry Platform]]**.
- **Certification Work**: Optional elective review: Databricks Certified Data Engineer Associate.
- **Monthly Milestone**: Complete implementation and record 5-minute architectural walkthrough video for Project 5.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Month 12*: [ ]

---

## 🗓️ Month 12: Technical Interview Sprints & Job Market Entry

- **Primary Objective**: Execute rigorous technical interview preparation and launch job application campaign.
- **Assigned Lessons**:
  - [[Interview Roadmap]]
  - [[50 High-Frequency SQL Drills]]
  - [[Python Data Wrangling Coding Bank]]
  - [[Systems Internals Question Defense]]
  - [[Behavioral STAR Incident Stories]]
  - [[Portfolio Presentation Playbook]]
  - [[Job-Ready Checklist]]
- **Skills Mastered**: Timed SQL live coding, Python data manipulation algorithms, system design defense, STAR behavioral storytelling, resume polish.
- **Practice Drills**: Complete all 50 SQL live coding interview drills; conduct 3 mock technical interviews with peers/mentors.
- **Portfolio Project Work**: Polish all 5 GitHub repositories (clean READMEs, Mermaid architectural diagrams, license, CI badges).
- **Certification Work**: Complete any outstanding certification objectives.
- **Monthly Milestone**: **100% completion of the [[Job-Ready Checklist|30-Point Job-Readiness Checklist]]**; begin submitting job applications.
- **Month Review Template*:
  - *What I learned*:
  - *What I struggled with*:
  - *Ready for Next Step*: [ ]
