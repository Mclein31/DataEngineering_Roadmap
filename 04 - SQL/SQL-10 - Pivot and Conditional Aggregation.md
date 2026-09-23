---
id: SQL-10
title: Pivot and Conditional Aggregation
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-10
---

# SQL-10 - Pivot and Conditional Aggregation

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Reshape datasets between normalized long and denormalized wide formats using portable standard SQL conditional aggregation.

## Concepts
- **Conditional Aggregation**: Combining `CASE WHEN` inside aggregate functions (`SUM(CASE WHEN ... THEN 1 ELSE 0 END)`).
- **The PostgreSQL `FILTER` Clause**: ANSI standard syntax (`COUNT(*) FILTER (WHERE status = 'FAILED')`) executing cleaner and faster than `CASE`.
- **Wide vs Long Layouts**: Converting vertical entity-attribute-value (EAV) records into horizontal analytical reporting columns.
- **Unpivoting**: Reshaping wide columns into long rows using `CROSS JOIN LATERAL` or `VALUES()`.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - Aggregate Expressions (FILTER)
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/sql-expressions.html#SYNTAX-AGGREGATES
- **Type**: Official Documentation
- **Topic**: Conditional Aggregation, FILTER Clause
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Transform a long monthly sales table into a wide format with columns for `jan_sales`, `feb_sales`, `mar_sales`, etc., using conditional aggregation.
- [ ] Rewrite conditional aggregation queries using the PostgreSQL `FILTER (WHERE ...)` clause.
- [ ] Unpivot wide quarterly metrics into normalized rows using `CROSS JOIN LATERAL (VALUES ...)`.

## Completion Criteria
- [ ] Reshape a dataset from long to wide format using standard portable SQL without vendor-specific pivot extensions.
- [ ] Use `FILTER (WHERE ...)` in PostgreSQL for multi-metric aggregation.
- [ ] Unpivot wide columns into normalized rows using `LATERAL`.

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
### FILTER Clause Pattern
```sql
SELECT 
    store_id,
    COUNT(*) as total_orders,
    COUNT(*) FILTER (WHERE status = 'COMPLETED') as completed_orders,
    COUNT(*) FILTER (WHERE status = 'RETURNED') as returned_orders,
    SUM(amount) FILTER (WHERE status = 'COMPLETED') as completed_revenue
FROM orders
GROUP BY store_id;
```

## Related Lessons
- Prerequisites: [[SQL-04 - Advanced Grouping Sets and Rollups]]
- Next Lesson: [[SQL-11 - Execution Plans with EXPLAIN]]
- Phase Overview: [[Phase 1 - Foundations]]
