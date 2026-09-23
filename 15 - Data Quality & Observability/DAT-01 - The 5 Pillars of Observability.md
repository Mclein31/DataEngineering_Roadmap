---
id: DAT-01
title: The 5 Pillars of Observability
phase: Phase 4
module: Module 15: Data Reliability Engineering & Observability
aliases:
  - DAT-01
---

# DAT-01 - The 5 Pillars of Observability

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand and monitor the 5 Pillars of Data Observability: Freshness, Volume, Schema, Distribution, and Lineage.

## Concepts
- **The Silent Data Bug Crisis**: Pipelines that execute successfully without raising exceptions but produce corrupt, duplicated, or stale data downstream.
- **The 5 Pillars of Observability**:
  1. *Freshness*: Has new data arrived within SLA? When was the table last updated?
  2. *Volume*: Is the expected number of records present? Did an upstream glitch drop 90% of rows?
  3. *Schema*: Have column names, types, or nullability changed without announcement?
  4. *Distribution*: Are numerical metrics and categories within expected statistical bounds (mean, variance, z-score)?
  5. *Lineage*: Upstream and downstream dependency mapping across tables, models, and dashboards.
- **Data Downtime**: The period when data is partial, incorrect, missing, or unavailable.

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 10: Data Operations and Observability)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Data Observability, 5 Pillars, Data Downtime
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Audit an existing retail dataset across all 5 observability pillars.
- [ ] Write SQL assertions measuring volume anomalies (comparing today's row count against a 7-day rolling average).
- [ ] Measure table freshness using `MAX(created_at)` vs `CURRENT_TIMESTAMP`.

## Completion Criteria
- [ ] Recite and define each of the 5 Pillars of Data Observability.
- [ ] Write SQL checks detecting volume anomalies (>30% drop from historical average).
- [ ] Articulate why pipeline success (exit code 0) does not guarantee data correctness.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Terraform & AWS CLI | IaC and cloud interaction | Yes (Native) | Yes | `brew install terraform awscli` | https://developer.hashicorp.com/terraform |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Volume Anomaly Detection Query
```sql
WITH daily_counts AS (
    SELECT DATE(created_at) as log_date, COUNT(*) as row_count
    FROM orders
    GROUP BY 1
),
stats AS (
    SELECT 
        log_date,
        row_count,
        AVG(row_count) OVER (ORDER BY log_date ROWS BETWEEN 7 PRECEDING AND 1 PRECEDING) as avg_7d
    FROM daily_counts
)
SELECT * FROM stats WHERE row_count < (avg_7d * 0.5); -- Alert if volume drops > 50%
```

## Related Lessons
- Prerequisites: [[DBT-07 - dbt Testing Framework]]
- Next Lesson: [[DAT-02 - Pipeline Testing with Soda Core]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
