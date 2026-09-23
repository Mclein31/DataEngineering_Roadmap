---
id: LAK-03
title: Limitations of Traditional Lakes
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-03
---

# LAK-03 - Limitations of Traditional Lakes

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand the critical failure modes of legacy raw directory-based Hive data lakes: lack of ACID transactions, dirty reads, and slow directory listings.

## Concepts
- **The Apache Hive Legacy Metastore Model**: Defining tables by directory paths on object storage (e.g., `s3://bucket/table/year=2026/month=09/`).
- **Core Failure Modes of Legacy Data Lakes**:
  - *No ACID Transactions*: A job writing 100 Parquet files that crashes halfway leaves half-written data visible to readers (dirty reads / corrupt pipelines).
  - *No Concurrency Guarantees*: Multiple writers mutating the same partition overwrite or interleave uncommitted files.
  - *Slow File Listing (`LIST` calls)*: Query planning requires recursively listing millions of files across S3 prefixes, taking minutes before query execution even begins.
  - *Fragile Physical Partitioning*: Changing partition schemes (e.g. from daily to hourly) requires rewriting the entire historical dataset on disk!

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 4: The Lakehouse Revolution)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Data Lake Flaws, Hive Metastore Limitations
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Simulate a concurrent write failure in a raw directory lake: start writing files, abort halfway, and observe that downstream queries read corrupt partial data.
- [ ] Measure the time taken by `aws s3 ls --recursive` on a prefix containing 50,000 files.

## Completion Criteria
- [ ] Explain why Hive metastores fail to provide atomic transactions on cloud object storage.
- [ ] Articulate the performance bottleneck of S3 `LIST` API calls during query planning.
- [ ] Describe the business risks of partial data commits in unversioned lakes.

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
### Hive Table vs Open Table Format
- **Hive Table**: Defined as a *directory of files*. Query planning = `LIST s3://bucket/dir/*`.
- **Open Table Format (Iceberg)**: Defined as a *canonical metadata tree of snapshots*. Query planning = reading Avro metadata files with zero `LIST` calls!

## Related Lessons
- Prerequisites: [[LAK-01 - Object Storage Architecture]]
- Next Lesson: [[LAK-04 - Open Table Format Paradigm]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
