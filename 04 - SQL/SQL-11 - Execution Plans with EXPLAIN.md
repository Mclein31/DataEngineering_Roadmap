---
id: SQL-11
title: Execution Plans with EXPLAIN
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-11
---

# SQL-11 - Execution Plans with EXPLAIN

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Read and analyze database query execution plans to identify bottlenecks, disk spills, misestimated rows, and sequential scans.

## Concepts
- **Execution Plan Mechanics**: `EXPLAIN (ANALYZE, BUFFERS, VERBOSE, SETTINGS)`:
  - `EXPLAIN`: Cost estimation based on planner statistics.
  - `ANALYZE`: Executes the query and records actual runtimes and memory allocations.
  - `BUFFERS`: Reports shared buffer hits, reads, and dirty writes.
- **Cost Metric (`cost=startup..total`)**: Arbitrary cost units where 1.0 represents a single sequential page disk read (`seq_page_cost`).
- **Rows Estimated vs Actual**: Diagnosing stale table statistics (`ANALYZE table_name`) when estimated rows differ by orders of magnitude from actual rows.
- **Planning Time vs Execution Time**: Distinguishing slow compilation from slow physical data execution.

## Learning Resource
- **Title**: Use The Index, Luke! - Execution Plans
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: EXPLAIN ANALYZE, Plan Costing, Optimization
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Seed a table with 1,000,000 rows without indexes.
- [ ] Run `EXPLAIN (ANALYZE, BUFFERS) SELECT * FROM table WHERE user_id = 45210;`.
- [ ] Identify the `Seq Scan` node, inspect total cost and buffer reads, create a B-Tree index, and re-run to verify the transition to `Index Scan`.

## Completion Criteria
- [ ] Identify a sequential scan on a table containing over 1 million records from execution plan output.
- [ ] Distinguish between planner estimation and actual runtime execution metrics.
- [ ] Interpret `shared hit` vs `read` metrics from the `BUFFERS` output.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Execution plan analysis | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community / pgAdmin | GUI database client | Yes | Yes | Free universal SQL client |

## Notes
### EXPLAIN Output Breakdown
```text
Seq Scan on large_orders  (cost=0.00..18450.00 rows=10 width=32) (actual time=0.045..85.231 rows=8 loops=1)
  Filter: (customer_id = 4821)
  Rows Removed by Filter: 999992
  Buffers: shared hit=8450
Planning Time: 0.120 ms
Execution Time: 85.310 ms
```

## Related Lessons
- Prerequisites: [[SQL-01 - Relational Execution Order]]
- Next Lesson: [[SQL-12 - Relational Access Methods]]
- Phase Overview: [[Phase 1 - Foundations]]
