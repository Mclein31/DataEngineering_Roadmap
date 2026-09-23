---
id: DB-05
title: Specialized PostgreSQL Indexes
phase: Phase 2
module: Module 05: Database Internals & Storage Engines
aliases:
  - DB-05
---

# DB-05 - Specialized PostgreSQL Indexes

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Deploy specialized PostgreSQL indexing architectures beyond standard B-Trees: GIN, GiST, BRIN, and Hash indexes.

## Concepts
- **GIN (Generalized Inverted Index)**: Designed for composite elements (arrays, full-text search, `jsonb` containment operators `@>`).
- **BRIN (Block Range Index)**: Stores min/max summaries per range of physical disk pages (e.g., 128 pages). Extremely compact (megabytes vs gigabytes) for naturally ordered time-series and append-only data.
- **GiST (Generalized Search Tree)**: Geometric, spatial (PostGIS), and range data (`tsrange`).
- **Hash Indexes**: Fast $O(1)$ equality lookups, write-ahead logged in modern PostgreSQL.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - Index Types
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/indexes-types.html
- **Type**: Official Documentation
- **Topic**: GIN, BRIN, GiST Indexes
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a 10M row time-series table ordered by `created_at`.
- [ ] Create a standard B-Tree index on `created_at` and compare its size to a BRIN index created with `pages_per_range = 128`.
- [ ] Store semi-structured user event payloads in a `jsonb` column and index it using a GIN index (`USING GIN (payload)`).

## Completion Criteria
- [ ] Compare disk footprints of a B-Tree vs BRIN index on a 10M row table (BRIN typically > 98% smaller).
- [ ] Accelerate JSON containment queries (`WHERE payload @> '{"status": "error"}'`) using a GIN index.
- [ ] Explain why BRIN indexes lose efficiency if table rows are not physically ordered on disk.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Index benchmarking | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### BRIN vs B-Tree Comparison
```sql
-- Standard B-Tree: High disk usage (~200MB for 10M rows)
CREATE INDEX idx_btree_ts ON sensor_readings (recorded_at);

-- BRIN Index: Tiny disk footprint (~100KB for 10M rows)
CREATE INDEX idx_brin_ts ON sensor_readings USING BRIN (recorded_at) WITH (pages_per_range = 128);
```

## Related Lessons
- Prerequisites: [[SQL-14 - Indexing Strategies and B-Trees]]
- Next Lesson: [[DB-06 - Analytical Engines ClickHouse and DuckDB]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
