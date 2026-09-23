---
id: DBT-02
title: Embedded Analytics with DuckDB
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-02
---

# DBT-02 - Embedded Analytics with DuckDB

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Leverage DuckDB for local, zero-cost development of production-grade analytical pipelines and dbt transformations.

## Concepts
- **DuckDB for Modern ELT**: Fast local execution without cloud billing; compiles and tests SQL models locally before cloud deployment.
- **Extensions Architecture**: `httpfs` (reading direct from S3/HTTP), `parquet`, `postgres_scanner` (direct reading from PostgreSQL tables without dump).
- **Direct Parquet & S3 Querying**: Reading, filtering, and joining Parquet files directly using standard ANSI SQL.
- **Integration with Python & dbt**: Using `dbt-duckdb` to build, snapshot, and test local dimensional data warehouses.

## Learning Resource
- **Title**: DuckDB Official Documentation
- **Provider / Author**: DuckDB Foundation
- **URL**: https://duckdb.org/docs/
- **Type**: Official Documentation
- **Topic**: DuckDB Architecture, Extensions, SQL
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install `dbt-duckdb`: `uv pip install dbt-core dbt-duckdb`.
- [ ] Use DuckDB CLI to attach to a PostgreSQL database and extract data directly to Parquet:
  `duckdb -c "INSTALL postgres; LOAD postgres; ATTACH 'host=localhost user=postgres password=postgres dbname=postgres' AS pg; COPY (SELECT * FROM pg.orders) TO 'orders.parquet' (FORMAT PARQUET);"`.
- [ ] Query the generated Parquet file in DuckDB with analytical window functions.

## Completion Criteria
- [ ] Extract tables from PostgreSQL to Parquet using DuckDB's postgres extension.
- [ ] Run analytical queries over local Parquet datasets using DuckDB.
- [ ] Configure `dbt-duckdb` profile for local pipeline execution.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Local analytics engine | Yes | Yes | `brew install duckdb` | https://duckdb.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### DuckDB Parquet Extraction
```sql
INSTALL postgres;
LOAD postgres;
ATTACH 'host=localhost port=5432 user=postgres password=postgres dbname=postgres' AS pg;
COPY (
    SELECT order_id, customer_id, total_amount, created_at 
    FROM pg.orders 
    WHERE created_at >= '2026-01-01'
) TO 'data/raw_orders.parquet' (FORMAT PARQUET, COMPRESSION ZSTD);
```

## Related Lessons
- Prerequisites: [[DBT-01 - Modern ELT Architecture]]
- Next Lesson: [[DBT-03 - dbt Core Setup and Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
