---
id: DW-04
title: Google BigQuery Architecture
phase: Phase 2
module: Module 08: Data Warehousing Fundamentals
aliases:
  - DW-04
---

# DW-04 - Google BigQuery Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Google BigQuery's serverless architecture: Dremel query engine, Colossus storage, Jupiter network, and Borg container management.

## Concepts
- **BigQuery's Serverless Primitives**:
  - *Dremel*: Multi-tenant distributed execution engine converting SQL into execution trees of mixers and leaf workers.
  - *Colossus*: Google's distributed file system storing data in Capacitor columnar format.
  - *Jupiter*: Petabit-scale bisection datacenter network allowing workers to read storage at 100Gbps+ without data locality constraints.
  - *Borg*: Google's container orchestrator dynamically allocating execution slots.
- **Slots & Execution Trees**: Dynamic allocation of query processing units (slots).
- **Billing Models**: On-Demand (priced per TB scanned) vs Capacity-Based (reserved slots).

## Learning Resource
- **Title**: Google Cloud BigQuery Architecture Overview
- **Provider / Author**: Google Cloud
- **URL**: https://cloud.google.com/bigquery/docs/architecture
- **Type**: Official Documentation
- **Topic**: BigQuery, Dremel, Serverless Analytics
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare BigQuery's true serverless architecture (no warehouse to size or start) against Snowflake's virtual warehouse provisioning model.
- [ ] Calculate the cost of running an unpartitioned `SELECT *` query on a 10TB table under on-demand pricing ($6.25 per TB).

## Completion Criteria
- [ ] Explain how BigQuery executes queries without requiring server provisioning.
- [ ] Identify the four Google hardware/software pillars powering BigQuery (Dremel, Colossus, Jupiter, Borg).
- [ ] Articulate the cost hazard of running `SELECT *` in on-demand BigQuery.

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
### BigQuery Cost Risk
On-Demand queries scan full columnar files for referenced fields:
```text
Scanning 5TB column without partition filter = 5 * $6.25 = $31.25 for a single query!
Partitioning by date reduces scan to 50GB = $0.31!
```

## Related Lessons
- Prerequisites: [[DW-01 - Cloud Warehouse Architecture]]
- Next Lesson: [[DW-05 - Partitioning and Clustering]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
