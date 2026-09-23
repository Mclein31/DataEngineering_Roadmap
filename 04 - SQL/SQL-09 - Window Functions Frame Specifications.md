---
id: SQL-09
title: Window Functions Frame Specifications
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-09
---

# SQL-09 - Window Functions Frame Specifications

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Compute moving averages and cumulative aggregates using explicit window frame bounds and avoid default frame performance pitfalls.

## Concepts
- **Window Frame Types**: `ROWS` (physical count of rows) vs `RANGE` (logical value offsets).
- **Frame Boundary Syntax**: `BETWEEN <start> AND <end>`:
  - `UNBOUNDED PRECEDING`, `n PRECEDING`, `CURRENT ROW`, `n FOLLOWING`, `UNBOUNDED FOLLOWING`.
- **The Default Window Frame Trap**: When `ORDER BY` is present without a frame clause, SQL defaults to `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`. This forces the engine to buffer and evaluate peers, causing severe performance degradation.
- **Rolling Aggregates**: Calculating 7-day or 30-day moving averages and cumulative running sums.

## Learning Resource
- **Title**: Use The Index, Luke! - Window Frames
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: Window Frames, ROWS vs RANGE
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compute a 7-day rolling moving average of active users using `ROWS BETWEEN 6 PRECEDING AND CURRENT ROW`.
- [ ] Compare query execution time and buffer usage between explicit `ROWS` and default `RANGE` over 1M rows using `EXPLAIN ANALYZE`.
- [ ] Compute a centered moving average using `ROWS BETWEEN 3 PRECEDING AND 3 FOLLOWING`.

## Completion Criteria
- [ ] Explain why the default window frame (`RANGE`) can severely degrade query performance compared to `ROWS`.
- [ ] Construct explicit moving average calculations with bounded frames.
- [ ] Articulate the difference between peer rows in `RANGE` and physical offsets in `ROWS`.

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
### Moving Average Frame
```sql
SELECT 
    metric_date,
    daily_revenue,
    AVG(daily_revenue) OVER (
        ORDER BY metric_date 
        ROWS BETWEEN 6 PRECEDING AND CURRENT ROW
    ) as moving_avg_7d
FROM revenue_metrics;
```

## Related Lessons
- Prerequisites: [[SQL-08 - Window Functions Value Navigation]]
- Next Lesson: [[SQL-10 - Pivot and Conditional Aggregation]]
- Phase Overview: [[Phase 1 - Foundations]]
