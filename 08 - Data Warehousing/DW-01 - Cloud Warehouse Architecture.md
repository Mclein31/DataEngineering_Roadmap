---
id: DW-01
title: Cloud Warehouse Architecture
phase: Phase 2
module: Module 08: Data Warehousing Fundamentals
aliases:
  - DW-01
---

# DW-01 - Cloud Warehouse Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand the architectural foundations of modern cloud data warehouses: shared-disk, shared-nothing, and multi-cluster shared-data.

## Concepts
- **Evolution of Warehouse Architectures**:
  - *Shared-Nothing (Legacy Redshift, Teradata)*: Compute nodes own specific disk slices; scaling requires full data re-sharding.
  - *Decoupled Storage & Compute (Snowflake, BigQuery)*: Centralized remote object storage (S3, GCS) with independent, ephemeral compute clusters.
- **Benefits of Compute Decoupling**: Auto-scaling clusters up/down in seconds, isolated compute clusters for ETL vs BI dashboards (zero resource contention).
- **Columnar Storage Optimization**: Micro-partitions, automatic pruning, and zero maintenance indexing.

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 4: Storage)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Cloud Warehouse Architecture, Decoupled Compute
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare architectural trade-offs between shared-nothing and decoupled storage/compute architectures.
- [ ] Explain why decoupled architectures completely eliminate the problem of BI queries slowing down daily ETL jobs.

## Completion Criteria
- [ ] Articulate the architectural differences between Snowflake and legacy MPP warehouses.
- [ ] Explain how compute auto-scaling operates independently of storage capacity.
- [ ] Describe micro-partitioning in modern cloud warehouses.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 (via Docker) | Relational database testing | Yes (Docker) | Yes | `docker run -d -p 5432:5432 postgres:16` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Decoupled Architecture
```text
  [ETL Virtual Warehouse]        [BI Virtual Warehouse]
            │                              │
            └───> [Central Cloud Storage] <───┘
                  (S3 / GCS / Azure Blob)
```

## Related Lessons
- Prerequisites: [[DBT-01 - Modern ELT Architecture]]
- Next Lesson: [[DW-02 - Snowflake Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
