---
id: DW-02
title: Snowflake Architecture
phase: Phase 2
module: Module 08: Data Warehousing Fundamentals
aliases:
  - DW-02
---

# DW-02 - Snowflake Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master the three-layer architecture of Snowflake: Cloud Services, Virtual Warehouses, and Hybrid Columnar Storage.

## Concepts
- **The 3 Snowflake Layers**:
  - *Cloud Services*: Authentication, query compilation, optimizer, access control, and metadata management.
  - *Virtual Warehouses*: Independent MPP compute clusters (T-shirt sizes XS to 6XL) that execute queries and cache data in local NVMe SSDs.
  - *Centralized Storage*: Persistent, compressed, immutable micro-partitions stored in cloud object storage.
- **Local NVMe SSD Caching**: Virtual warehouse local disk caching accelerating repeated query reads without touching cloud object storage.
- **Credit Consumption Mechanics**: Sizing warehouses, auto-suspend (`auto_suspend = 60`), and auto-resume to prevent runaway cloud bills.

## Learning Resource
- **Title**: Snowflake Official Documentation & Architecture Overview
- **Provider / Author**: Snowflake Inc.
- **URL**: https://docs.snowflake.com/en/user-guide/intro-key-concepts
- **Type**: Official Documentation
- **Topic**: Snowflake Architecture, Micro-Partitions, Virtual Warehouses
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Review virtual warehouse sizing rules and credit consumption scales (XS=1 credit/hr, S=2, M=4, L=8).
- [ ] Write SQL DDL configuring a virtual warehouse with `AUTO_SUSPEND = 60` and `AUTO_RESUME = TRUE`.

## Completion Criteria
- [ ] Explain the responsibilities of Snowflake's 3 architectural layers.
- [ ] Configure auto-suspend policies to eliminate idle compute credit waste.
- [ ] Describe how micro-partition metadata enables partition pruning without user-defined indexes.

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
### Warehouse Configuration
```sql
CREATE WAREHOUSE analytics_wh WITH
    WAREHOUSE_SIZE = 'XSMALL'
    AUTO_SUSPEND = 60
    AUTO_RESUME = TRUE
    INITIALLY_SUSPENDED = TRUE;
```

## Related Lessons
- Prerequisites: [[DW-01 - Cloud Warehouse Architecture]]
- Next Lesson: [[DW-03 - Snowflake Time Travel and Cloning]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
