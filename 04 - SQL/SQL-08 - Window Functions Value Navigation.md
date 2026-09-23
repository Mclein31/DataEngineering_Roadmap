---
id: SQL-08
title: Window Functions Value Navigation
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-08
---

# SQL-08 - Window Functions Value Navigation

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Perform time-series difference, period-over-period growth, and lead/lag calculations directly in SQL without self-joins.

## Concepts
- **Value Navigation Functions**:
  - `LEAD(col, offset, default)`: Access subsequent rows at fixed offset.
  - `LAG(col, offset, default)`: Access preceding rows at fixed offset.
  - `FIRST_VALUE(col)` / `LAST_VALUE(col)`: Access boundary values in the frame.
- **Time-Series Metric Calculations**: Calculating Month-over-Month (MoM) growth rates and dormancy gaps.
- **Default Value Fallbacks**: Providing safe replacement values to prevent `NULL` division errors.

## Learning Resource
- **Title**: Use The Index, Luke! - Value Windowing
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: Lead, Lag, First_Value
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Calculate Day-over-Day percentage revenue change for an e-commerce platform using `LAG()`.
- [ ] Calculate duration in minutes between a user's consecutive clickstream events.
- [ ] Identify customers with more than 60 days of inactivity between consecutive purchases.

## Completion Criteria
- [ ] Calculate period-over-period growth metrics using `LAG()`.
- [ ] Compute session duration differences between consecutive records.
- [ ] Provide default zero fallbacks for initial records using `LAG(val, 1, 0)`.

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
### Day-over-Day Revenue Growth
```sql
SELECT 
    sale_date,
    revenue,
    LAG(revenue, 1) OVER (ORDER BY sale_date) as prev_day_revenue,
    ROUND(
        ((revenue - LAG(revenue, 1) OVER (ORDER BY sale_date)) / 
        NULLIF(LAG(revenue, 1) OVER (ORDER BY sale_date), 0)) * 100, 
        2
    ) as dod_growth_pct
FROM daily_revenue;
```

## Related Lessons
- Prerequisites: [[SQL-07 - Window Functions Ranking]]
- Next Lesson: [[SQL-09 - Window Functions Frame Specifications]]
- Phase Overview: [[Phase 1 - Foundations]]
