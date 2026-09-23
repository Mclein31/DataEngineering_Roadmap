---
id: SQL-12
title: Relational Access Methods
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-12
---

# SQL-12 - Relational Access Methods

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand how the relational storage engine reads tuples from disk into shared memory buffers across access methods.

## Concepts
- **Relational Access Methods**:
  - **Sequential Scan (`Seq Scan`)**: Reading every page sequentially from disk; fast for scanning > 20% of a table due to OS read-ahead.
  - **Index Scan**: Traversing B-Tree index to fetch tuple pointers (TIDs), then fetching corresponding heap table pages.
  - **Bitmap Index Scan & Bitmap Heap Scan**: Generating an in-memory bitmap of matching page numbers from the index, then reading heap pages in physical disk order to minimize random I/O.
  - **Index Only Scan**: Returning results entirely from index leaves without touching heap tables (requires up-to-date visibility map).

## Learning Resource
- **Title**: Use The Index, Luke! - Access Paths
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: Access Methods, Scans, Heap Lookups
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Design an index and query combination that forces PostgreSQL to perform an `Index Only Scan`.
- [ ] Verify that `Heap Fetches: 0` appears in the execution plan.
- [ ] Write a range query that triggers a `Bitmap Index Scan` and inspect how `work_mem` impacts bitmap construction.

## Completion Criteria
- [ ] Explain why the planner chooses a Sequential Scan over an Index Scan when querying > 20% of a table.
- [ ] Force and verify an `Index Only Scan` with zero heap fetches.
- [ ] Differentiate between an `Index Scan` and a `Bitmap Heap Scan`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Relational testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community / pgAdmin | GUI database client | Yes | Yes | Free universal SQL client |

## Notes
### Index Only Scan Requirements
1. Every column referenced in `SELECT` and `WHERE` must be present in the index.
2. The Visibility Map must confirm that all tuples on the page are visible to all current transactions (verified via `VACUUM`).

## Related Lessons
- Prerequisites: [[SQL-11 - Execution Plans with EXPLAIN]]
- Next Lesson: [[SQL-13 - Join Algorithms]]
- Phase Overview: [[Phase 1 - Foundations]]
