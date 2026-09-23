---
id: DB-06
title: Analytical Engines ClickHouse and DuckDB
phase: Phase 2
module: Module 05: Database Internals & Storage Engines
aliases:
  - DB-06
---

# DB-06 - Analytical Engines ClickHouse and DuckDB

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand the architecture of dedicated modern OLAP engines: embedded in-process DuckDB and distributed ClickHouse.

## Concepts
- **The Rise of In-Process OLAP (DuckDB)**: "The SQLite for Analytics". Zero external server process, runs embedded inside Python/CLI, operates directly on Parquet and CSV files with zero-copy Arrow integration.
- **Vectorized Execution Engines**: Processing data in vector vectors (morsels of 2048 rows) that fit in L1/L2 CPU caches.
- **ClickHouse Architecture**: Distributed MergeTree engine family, primary sorting keys, sparse primary index, and data part compaction.
- **Trade-Offs**: When to use embedded DuckDB (< 1TB) vs distributed ClickHouse/Spark (> 1TB).

## Learning Resource
- **Title**: DuckDB Official Documentation
- **Provider / Author**: DuckDB Foundation
- **URL**: https://duckdb.org/docs/
- **Type**: Official Documentation
- **Topic**: In-Process OLAP, Columnar Vectorization
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install DuckDB CLI: `brew install duckdb`.
- [ ] Query a multi-gigabyte public Parquet file directly from S3 or local disk without loading it into a table:
  `duckdb -c "SELECT COUNT(*), AVG(fare_amount) FROM 'yellow_tripdata_*.parquet';"`.
- [ ] Execute an analytical aggregation in DuckDB from Python using `duckdb.sql()` and export directly to a Polars DataFrame.

## Completion Criteria
- [ ] Query Parquet files directly from SQL using DuckDB without prior table creation.
- [ ] Explain how DuckDB achieves low-latency analytics without running a daemon.
- [ ] Articulate the architectural difference between sparse indexing in ClickHouse and dense B-Trees in Postgres.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Analytical querying | Yes (Native) | Yes | `brew install duckdb` | https://duckdb.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### DuckDB Zero-Copy Querying
```python
import duckdb

# Query Parquet files directly using vectorized SQL
res = duckdb.query('''
    SELECT 
        passenger_count, 
        ROUND(AVG(trip_distance), 2) as avg_distance,
        ROUND(AVG(total_amount), 2) as avg_fare
    FROM 'data/taxi_*.parquet'
    GROUP BY 1
    ORDER BY 1
''').pl() # Convert directly to Polars LazyFrame with zero memory copy
```

## Related Lessons
- Prerequisites: [[DB-01 - Row vs Columnar Storage]]
- Next Lesson: [[MOD-01 - Relational Normalization 1NF to 3NF]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
