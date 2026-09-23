---
id: DAT-06
title: Anomaly Detection and Alerting
phase: Phase 4
module: Module 15: Data Reliability Engineering & Observability
aliases:
  - DAT-06
---

# DAT-06 - Anomaly Detection and Alerting

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build automated statistical anomaly detection engines tracking metric drift and dispatching actionable Slack/PagerDuty alerts.

## Concepts
- **Statistical Anomaly Detection**:
  - *Z-Score*: Measuring deviations from historical mean ($Z = (X - \mu) / \sigma$). Flags anomalies when $|Z| > 3$.
  - *Interquartile Range (IQR)*: Outlier detection robust against extreme skewed distributions.
  - *Rolling Window Baselines*: Calculating dynamic expected bounds based on day-of-week seasonality (e.g., comparing Monday to previous Mondays).
- **Alert Fatigue Prevention**: Tuning sensitivity thresholds, grouping related alerts into a single incident, and avoiding alerts on benign volume fluctuations.
- **Incident Escalation**: Routing actionable alerts with diagnostic context: failed check, affected dataset, run ID, and rerun commands.

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 10: Security, Privacy, and Ops)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Anomaly Detection, Alerting, Incident Management
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Implement a Python function computing rolling 30-day Z-scores over daily ingestion metrics.
- [ ] Flag synthetic volume drops where $|Z| > 2.5$.
- [ ] Format an actionable webhook alert containing run ID, timestamp, and query links for immediate team triage.

## Completion Criteria
- [ ] Implement Z-score anomaly detection in Python or SQL.
- [ ] Account for day-of-week seasonality in baseline calculations.
- [ ] Design an actionable incident notification template minimizing alert fatigue.

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
### Z-Score Anomaly Calculation in SQL
```sql
WITH daily_stats AS (
    SELECT 
        log_date,
        daily_revenue,
        AVG(daily_revenue) OVER (ORDER BY log_date ROWS BETWEEN 30 PRECEDING AND 1 PRECEDING) as mean_rev,
        STDDEV(daily_revenue) OVER (ORDER BY log_date ROWS BETWEEN 30 PRECEDING AND 1 PRECEDING) as std_rev
    FROM revenue_metrics
)
SELECT 
    log_date, 
    daily_revenue, 
    mean_rev,
    ROUND((daily_revenue - mean_rev) / NULLIF(std_rev, 0), 2) as z_score
FROM daily_stats
WHERE ABS((daily_revenue - mean_rev) / NULLIF(std_rev, 0)) > 3.0;
```

## Related Lessons
- Prerequisites: [[DAT-01 - The 5 Pillars of Observability]]
- Next Lesson: [[GOV-01 - Access Control Models RBAC ABAC]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
