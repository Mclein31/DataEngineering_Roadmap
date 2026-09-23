---
id: SQL-07
title: Window Functions Ranking
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-07
---

# SQL-07 - Window Functions Ranking

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Partition datasets and rank records within groups without collapsing row granularity using window ranking functions.

## Concepts
- **The Window Clause (`OVER`)**: `PARTITION BY` (grouping scope) and `ORDER BY` (sorting sequence inside the partition).
- **Ranking Functions**:
  - `ROW_NUMBER()`: Unique sequential integer for every row (arbitrary tiebreaker).
  - `RANK()`: Assigns identical ranks to ties, skipping subsequent ranks (1, 2, 2, 4).
  - `DENSE_RANK()`: Assigns identical ranks to ties without skipping subsequent ranks (1, 2, 2, 3).
  - `NTILE(n)`: Divides partition into $n$ roughly equal buckets (quartiles, deciles, percentiles).

## Learning Resource
- **Title**: Use The Index, Luke! - Window Functions
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: Window Functions, Ranking Mechanics
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write a query finding the top 3 highest-earning employees per department using `DENSE_RANK()`.
- [ ] Demonstrate deduplication using `ROW_NUMBER() OVER (PARTITION BY key ORDER BY timestamp DESC)`.
- [ ] Calculate customer spend quartiles using `NTILE(4)`.

## Completion Criteria
- [ ] Articulate the exact difference between `ROW_NUMBER()`, `RANK()`, and `DENSE_RANK()` when duplicate values occur.
- [ ] Write a query that extracts the top N records per partition.
- [ ] Explain why window functions execute after `WHERE` and `GROUP BY` but before `ORDER BY`.

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
### Ranking Comparison Table
| Value | ROW_NUMBER() | RANK() | DENSE_RANK() |
| :--- | :--- | :--- | :--- |
| 100 | 1 | 1 | 1 |
| 90 | 2 | 2 | 2 |
| 90 | 3 | 2 | 2 |
| 80 | 4 | 4 | 3 |

## Related Lessons
- Prerequisites: [[SQL-01 - Relational Execution Order]]
- Next Lesson: [[SQL-08 - Window Functions Value Navigation]]
- Phase Overview: [[Phase 1 - Foundations]]
