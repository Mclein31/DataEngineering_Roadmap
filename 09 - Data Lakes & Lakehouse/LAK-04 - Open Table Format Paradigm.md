---
id: LAK-04
title: Open Table Format Paradigm
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-04
---

# LAK-04 - Open Table Format Paradigm

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand how Open Table Formats (Iceberg, Delta Lake, Hudi) bring full ACID transaction guarantees to cloud object storage.

## Concepts
- **The Open Table Format (OTF) Revolution**: Decoupling the storage format (Parquet/ORC) from table metadata management.
- **ACID Guarantees on Object Storage**:
  - *Atomicity*: Commits occur via atomic metadata pointer swap; all files in a commit become visible simultaneously or none do.
  - *Consistency*: Snapshot isolation guarantees readers only see fully committed snapshots.
  - *Isolation*: Optimistic Concurrency Control (OCC) detecting conflicting writes.
  - *Durability*: Stored directly on durable cloud object storage (S3/MinIO).
- **The Modern Triad**: Apache Iceberg, Delta Lake (Linux Foundation), and Apache Hudi.

## Learning Resource
- **Title**: Apache Iceberg: The Definitive Guide (Chapter 1 & 2)
- **Provider / Author**: Tomer Shiran, Jason Hughes, Alex Merced
- **URL**: https://www.dremio.com/resources/guides/apache-iceberg-the-definitive-guide/
- **Type**: Free Official eBook
- **Topic**: Open Table Formats, ACID, Snapshot Isolation
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare features across Iceberg, Delta Lake, and Hudi in a comparison matrix.
- [ ] Understand why Apache Iceberg emerged as the multi-engine standard (supported natively by Snowflake, Spark, Trino, Flink, DuckDB, BigQuery).

## Completion Criteria
- [ ] Define the 4 ACID properties in the context of open lakehouses.
- [ ] Explain how Optimistic Concurrency Control (OCC) resolves concurrent write conflicts.
- [ ] Differentiate between file formats (Parquet) and table formats (Iceberg).

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
### Open Table Format Triad
| Feature | Apache Iceberg | Delta Lake | Apache Hudi |
| :--- | :--- | :--- | :--- |
| **Governance** | Apache Software Foundation | Linux Foundation | Apache Software Foundation |
| **Catalog Independence** | Exceptional (REST, Nessie, Polaris) | Tied closely to Unity / Hive | Hive / AWS Glue |
| **Partitioning** | Hidden Partitioning (Best-in-class) | Generated columns / Liquid clustering | Physical directory based |

## Related Lessons
- Prerequisites: [[LAK-03 - Limitations of Traditional Lakes]]
- Next Lesson: [[LAK-05 - Apache Iceberg Architecture]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
