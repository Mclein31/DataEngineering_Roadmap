---
id: SQL-02
title: Filtering and Three-Valued Logic
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-02
---

# SQL-02 - Filtering and Three-Valued Logic

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Avoid data loss and silent query bugs caused by NULL behavior and three-valued logic in relational expressions.

## Concepts
- **Three-Valued Logic (3VL)**: Truth values in SQL evaluate to `TRUE`, `FALSE`, or `UNKNOWN`. Any equality comparison with `NULL` (`col = NULL` or `col != NULL`) evaluates to `UNKNOWN`.
- **The Catastrophic `NOT IN` with NULL Trap**: If a subquery `NOT IN (SELECT id FROM ...)` returns even a single `NULL`, the entire predicate evaluates to `UNKNOWN` and returns 0 rows!
- **Null-Safe Comparisons**: `IS NULL`, `IS NOT NULL`, `IS DISTINCT FROM`, `COALESCE`, `NULLIF`.

## Learning Resource
- **Title**: Select Star SQL (NULLs and Three-Valued Logic)
- **Provider / Author**: Zi Chong Kao
- **URL**: https://selectstarsql.com/
- **Type**: Free Interactive Book
- **Topic**: Three-Valued Logic, NULL handling
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a table with nullable IDs and populate sample data containing nulls.
- [ ] Execute `SELECT * FROM table WHERE id NOT IN (SELECT id FROM other_table)` where `other_table` has a null; observe 0 rows returned.
- [ ] Refactor the query to use `NOT EXISTS` and verify correct records are returned.

## Completion Criteria
- [ ] Explain why `NOT IN (NULL)` evaluates to empty results.
- [ ] Differentiate between `IS DISTINCT FROM` and standard `=` in PostgreSQL.
- [ ] Correctly replace fragile `NOT IN` subqueries with `NOT EXISTS` or `LEFT JOIN ... WHERE rhs.id IS NULL`.

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
### The `NOT IN` Danger & Fix
```sql
-- DANGEROUS: If any customer_id is NULL, returns 0 rows
SELECT * FROM orders WHERE customer_id NOT IN (SELECT customer_id FROM vip_customers);

-- SAFE & PERFORMANT:
SELECT o.* 
FROM orders o 
WHERE NOT EXISTS (
    SELECT 1 FROM vip_customers v WHERE v.customer_id = o.customer_id
);
```

## Related Lessons
- Prerequisites: [[SQL-01 - Relational Execution Order]]
- Next Lesson: [[SQL-03 - Relational Joins and Anti-Joins]]
- Phase Overview: [[Phase 1 - Foundations]]
