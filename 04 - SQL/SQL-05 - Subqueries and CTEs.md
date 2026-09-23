---
id: SQL-05
title: Subqueries and CTEs
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-05
---

# SQL-05 - Subqueries and CTEs

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Structure complex analytical pipelines into readable, modular SQL using Common Table Expressions (CTEs) and optimize query boundaries.

## Concepts
- **Subquery Types**: Scalar subqueries (returning single value), row subqueries, correlated subqueries (evaluated per outer tuple).
- **Common Table Expressions (CTEs)**: Defining named temporary result sets via `WITH` clauses for modularity.
- **Optimization Fences & Materialization**: In PostgreSQL 12+, CTEs are automatically inlined by default. Using `AS MATERIALIZED` forces the database to evaluate the CTE once into a temporary buffer.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - WITH Queries (Common Table Expressions)
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/queries-with.html
- **Type**: Official Documentation
- **Topic**: CTEs, Subqueries, Query Optimization
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Refactor a deeply nested 4-level correlated subquery into a linear sequence of named CTEs.
- [ ] Inspect execution plans comparing an inlined CTE vs `WITH ... AS MATERIALIZED`.
- [ ] Write a CTE that performs data deduplication before passing clean tuples to downstream join logic.

## Completion Criteria
- [ ] Refactor deep subqueries into readable CTE pipelines conforming to standard style guides.
- [ ] Explain when to force `WITH ... AS MATERIALIZED` in PostgreSQL to prevent expensive re-evaluation.
- [ ] Identify when an optimizer inlines a CTE using `EXPLAIN`.

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
### Materialized vs Inlined CTE
```sql
-- Forces evaluation into temporary memory buffer (prevents multiple evaluations)
WITH cached_aggregations AS MATERIALIZED (
    SELECT customer_id, SUM(amount) as lifetime_spend
    FROM orders
    GROUP BY customer_id
)
SELECT * FROM cached_aggregations WHERE lifetime_spend > 1000;
```

## Related Lessons
- Prerequisites: [[SQL-03 - Relational Joins and Anti-Joins]]
- Next Lesson: [[SQL-06 - Recursive CTEs]]
- Phase Overview: [[Phase 1 - Foundations]]
