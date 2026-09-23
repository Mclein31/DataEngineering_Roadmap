---
id: LAK-07
title: Delta Lake and UniForm
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-07
---

# LAK-07 - Delta Lake and UniForm

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Delta Lake architecture (`_delta_log`), transaction serialization, and Universal Format (UniForm) cross-reader compatibility.

## Concepts
- **Delta Lake Architecture**:
  - `_delta_log/`: Directory storing sequential JSON commit logs (`000000.json`, `000001.json`).
  - Checkpoint Parquet Files: Every 10 commits, Delta writes a multi-commit Parquet checkpoint consolidating past log entries.
- **ACID Operations**: `OPTIMIZE` (file compaction), `Z-ORDER BY` (multi-dimensional clustering), `VACUUM` (removing tombstoned files past retention).
- **Universal Format (UniForm)**: Generates metadata for Iceberg and Hudi alongside Delta Lake logs without duplicating Parquet data files, enabling any Iceberg engine to read Delta tables directly.

## Learning Resource
- **Title**: Delta Lake Official Documentation
- **Provider / Author**: Linux Foundation / Databricks
- **URL**: https://docs.delta.io/latest/index.html
- **Type**: Official Documentation
- **Topic**: Delta Lake, Transaction Log, UniForm
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Inspect the contents of `_delta_log/000000.json` to view commit action records (`add`, `remove`, `commitInfo`).
- [ ] Execute `OPTIMIZE orders ZORDER BY (customer_id)` in PySpark.
- [ ] Run `VACUUM orders RETAIN 168 HOURS` to delete old tombstoned Parquet files.

## Completion Criteria
- [ ] Explain how Delta Lake uses JSON logs and Parquet checkpoints for transaction resolution.
- [ ] Articulate how UniForm bridges Delta Lake and Apache Iceberg ecosystems.
- [ ] Explain the safety purpose of `VACUUM` retention thresholds.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker / MinIO | Local object storage & service container | Yes | Yes | `brew install --cask docker` | https://min.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Direct Parquet/Iceberg querying | Yes | Yes | `brew install duckdb` |

## Notes
### Delta Transaction Log Structure
```text
table_dir/
├── _delta_log/
│   ├── 000000.json (Commit 0: add files)
│   ├── 000001.json (Commit 1: update/remove files)
│   └── 000010.checkpoint.parquet (Consolidated state)
├── part-00000.parquet
└── part-00001.parquet
```

## Related Lessons
- Prerequisites: [[LAK-05 - Apache Iceberg Architecture]]
- Next Lesson: [[LAK-08 - Open Table Catalogs]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
