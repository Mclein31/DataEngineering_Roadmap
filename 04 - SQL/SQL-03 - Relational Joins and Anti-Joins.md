---
id: SQL-03
title: Relational Joins and Anti-Joins
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-03
---

# SQL-03 - Relational Joins and Anti-Joins

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Join disparate tables without introducing Cartesian products or unintentional record drops using inner, outer, cross, and anti-joins.

## Concepts
- **Join Types**: `INNER`, `LEFT`, `RIGHT`, `FULL OUTER`, and `CROSS JOIN` (Cartesian product).
- **Anti-Joins & Semi-Joins**: Identifying records in table A that have no matching records in table B (`LEFT JOIN ... WHERE rhs.key IS NULL` vs `NOT EXISTS`).
- **The Accidental Inner Join Trap**: Placing a filter on the right-hand table in the `WHERE` clause instead of the `ON` clause, silently converting a `LEFT JOIN` into an `INNER JOIN`.
- **Self-Joins**: Joining a table to itself to compare rows within the same table (e.g., manager-employee relationships).

## Learning Resource
- **Title**: Select Star SQL (Joins & Sets)
- **Provider / Author**: Zi Chong Kao
- **URL**: https://selectstarsql.com/
- **Type**: Free Interactive Book
- **Topic**: Joins, Anti-Joins, Venn Semantics
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Find all customers who have never placed an order using both an anti-join and a `NOT EXISTS` clause.
- [ ] Compare query execution plans using `EXPLAIN ANALYZE` for both approaches.
- [ ] Demonstrate how `WHERE rhs.col = 'active'` converts a `LEFT JOIN` into an `INNER JOIN`.

## Completion Criteria
- [ ] Explain why placing right-table predicates in `WHERE` breaks outer joins.
- [ ] Write anti-join queries returning unmatched records.
- [ ] Construct a cross-join to generate a complete date/store Cartesian grid for missing value analysis.

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
### Anti-Join Comparison
```sql
-- Approach 1: LEFT JOIN with IS NULL
SELECT c.customer_id, c.name
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;

-- Approach 2: NOT EXISTS (Often optimized more efficiently by planner)
SELECT c.customer_id, c.name
FROM customers c
WHERE NOT EXISTS (
    SELECT 1 FROM orders o WHERE o.customer_id = c.customer_id
);
```

## Related Lessons
- Prerequisites: [[SQL-02 - Filtering and Three-Valued Logic]]
- Next Lesson: [[SQL-04 - Advanced Grouping Sets and Rollups]]
- Phase Overview: [[Phase 1 - Foundations]]
