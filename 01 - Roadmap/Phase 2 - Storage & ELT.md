---
title: Phase 2 - Storage, Modeling & Modern ELT
phase: Phase 2
duration: Months 4–5 (8 Weeks)
aliases:
  - Phase 2
  - Phase 2 - Storage & ELT
---

# 🗄️ Phase 2: Storage, Modeling & Modern ELT

## Overview
Phase 2 bridges the gap between raw data storage and business analytics. You will learn how database engines store bytes on disk (row pages vs columnar blocks), how WAL and MVCC guarantee ACID transactions, how to architect Kimball star schemas and Slowly Changing Dimensions (SCD), and how to build automated local data transformation pipelines using DuckDB and `dbt-core`.

---

## 🎯 Target Capabilities
- Understand low-level database storage: row slotted pages, columnar compression (run-length, dictionary), and MVCC concurrency controls.
- Diagnose and eliminate query bottlenecks using PostgreSQL `EXPLAIN (ANALYZE, BUFFERS)` and composite B-Tree indexes.
- Design normalized OLTP schemas (3NF) and denormalized analytical OLAP schemas (Kimball Star Schema).
- Implement Slowly Changing Dimensions (SCD Type 1, Type 2, and Type 3) to accurately preserve historical attributes over time.
- Structure warehouse transformations following the Medallion Architecture (Bronze landing -> Silver cleaned -> Gold business marts).
- Build automated, tested in-warehouse transformation pipelines using `dbt-core` and DuckDB.
- Write robust generic schema assertions and singular custom SQL tests that halt pipeline progression on dirty data.
- Understand cloud warehouse storage/compute decoupling and cost governance mechanisms in Snowflake and Google BigQuery.

---

## 📚 Modules in Phase 2
- **Module 05: Database Internals & Storage Engines**
  - [[DB-01 - Row vs Columnar Storage]]
  - [[DB-02 - Write-Ahead Logging and Durability]]
  - [[DB-03 - MVCC and Isolation Levels]]
  - [[DB-04 - PostgreSQL Vacuum and Bloat]]
  - [[DB-05 - Specialized PostgreSQL Indexes]]
  - [[DB-06 - Analytical Engines ClickHouse and DuckDB]]
- **Module 06: Data Modeling & Schema Design**
  - [[MOD-01 - Relational Normalization 1NF to 3NF]]
  - [[MOD-02 - Kimball Dimensional Modeling]]
  - [[MOD-03 - Fact Table Architecture]]
  - [[MOD-04 - Dimension Table Architecture]]
  - [[MOD-05 - Slowly Changing Dimensions]]
  - [[MOD-06 - Medallion Architecture]]
  - [[MOD-07 - Data Vault 2 Basics]]
  - [[MOD-08 - One Big Table vs Star Schema]]
- **Module 07: Modern In-Warehouse ELT & dbt**
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
- **Module 08: Cloud Data Warehousing Fundamentals**
  - [[DW-01 - Cloud Warehouse Architecture]]
  - [[DW-02 - Snowflake Architecture]]
  - [[DW-03 - Snowflake Time Travel and Cloning]]
  - [[DW-04 - Google BigQuery Architecture]]
  - [[DW-05 - Partitioning and Clustering]]
  - [[DW-06 - Warehouse Cost Governance]]

---

## 🏆 Milestone Gate 2 Exit Criteria
- [ ] Deliver **[[Project 1 - Local Modern ELT Pipeline/README|Project 1: Local Modern ELT Pipeline (Retail Analytics)]]** with PostgreSQL, DuckDB, `dbt-core`, and Metabase.
- [ ] Verify that `dbt build` runs cleanly with 100% passing tests (zero schema or custom test failures).
- [ ] Optimize an unindexed query on a 5M row PostgreSQL table, reducing runtime by $>80\%$.
