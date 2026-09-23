---
id: SQL-01
title: Relational Execution Order
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-01
---

# SQL-01 - Relational Execution Order

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Write queries understanding how the SQL engine parses, binds, optimizes, and executes clauses logically.

## Concepts
- **Logical Query Processing Order**:
  `1. FROM` -> `2. ON` -> `3. JOIN` -> `4. WHERE` -> `5. GROUP BY` -> `6. WITH CUBE/ROLLUP` -> `7. HAVING` -> `8. SELECT` -> `9. DISTINCT` -> `10. ORDER BY` -> `11. LIMIT / OFFSET`.
- **The Alias Binding Paradox**: Why column aliases created in `SELECT` cannot be referenced in `WHERE` or `GROUP BY` (because `WHERE` and `GROUP BY` execute before `SELECT`).
- **`WHERE` vs `HAVING` Mechanics**: `WHERE` filters raw tuples before aggregation; `HAVING` filters aggregated grouped rows after `GROUP BY`.

## Learning Resource
- **Title**: Select Star SQL
- **Provider / Author**: Zi Chong Kao
- **URL**: https://selectstarsql.com/
- **Type**: Free Interactive Book
- **Topic**: Practical SQL, Logical Execution Order
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Launch local Postgres container: `docker run --name de-postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:16`.
- [ ] Connect via `psql -h localhost -U postgres` and create a dummy sales table.
- [ ] Write a query demonstrating that referencing a `SELECT` column alias in the `WHERE` clause fails with `column does not exist`.

## Completion Criteria
- [ ] Recite the 11 logical query processing steps in exact order.
- [ ] Explain why `WHERE` cannot evaluate aggregate functions like `SUM()` or `COUNT()`.
- [ ] Write queries correctly placing filters in `WHERE` vs `HAVING` to optimize aggregation performance.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 (via Docker) | Relational query execution | Yes (Docker) | Yes | `docker run -p 5432:5432 -d postgres:16` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community / pgAdmin | GUI database client | Yes | Yes | Free universal SQL client |

## Notes
### Logical Processing Order Diagram
```text
FROM & JOINs  (Identify candidate datasets)
    ↓
WHERE         (Filter raw rows before grouping)
    ↓
GROUP BY      (Form aggregated rows)
    ↓
HAVING        (Filter aggregated rows)
    ↓
SELECT        (Compute projections and expressions)
    ↓
DISTINCT      (Deduplicate result set)
    ↓
ORDER BY      (Sort final output)
    ↓
LIMIT         (Slice top N records)
```

## Related Lessons
- Prerequisites: None
- Next Lesson: [[SQL-02 - Filtering and Three-Valued Logic]]
- Phase Overview: [[Phase 1 - Foundations]]
