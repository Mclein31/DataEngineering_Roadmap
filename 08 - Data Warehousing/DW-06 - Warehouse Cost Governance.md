---
id: DW-06
title: Warehouse Cost Governance
phase: Phase 2
module: Module 08: Data Warehousing Fundamentals
aliases:
  - DW-06
---

# DW-06 - Warehouse Cost Governance

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement strict cost controls, resource monitors, query timeouts, and budget guardrails to prevent runaway cloud warehouse invoices.

## Concepts
- **The Danger of Elastic Cloud Billing**: How poorly written queries, Cartesian joins, or unmonitored loops can generate thousands of dollars in cloud charges overnight.
- **Snowflake Resource Monitors**: Setting credit quotas, notification thresholds (75%, 90%), and hard shutdown actions (100% suspend warehouse).
- **BigQuery Maximum Bytes Billed**: Using client-side safety constraints (`maximum_bytes_billed`) to abort any query that would scan more than a set threshold (e.g., 50GB).
- **Query Timeouts**: Enforcing statement timeouts (`STATEMENT_TIMEOUT_IN_SECONDS = 3600`) to automatically kill hung queries.

## Learning Resource
- **Title**: Snowflake Documentation - Working with Resource Monitors
- **Provider / Author**: Snowflake Inc.
- **URL**: https://docs.snowflake.com/en/user-guide/resource-monitors
- **Type**: Official Documentation
- **Topic**: Cost Governance, Resource Monitors, Quotas
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write SQL creating a Snowflake Resource Monitor alerting at 80% and immediately suspending compute at 100% credit quota.
- [ ] Configure `maximum_bytes_billed` in BigQuery Python SDK to fail any query scanning > 10GB.
- [ ] Audit slow and expensive queries using `INFORMATION_SCHEMA.QUERY_HISTORY`.

## Completion Criteria
- [ ] Configure a Resource Monitor in Snowflake with automated suspension policies.
- [ ] Implement query cost guardrails using byte-scan limits in BigQuery.
- [ ] Query metadata history tables to detect the top 5 most expensive queries over the last 30 days.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 (via Docker) | Relational database testing | Yes (Docker) | Yes | `docker run -d -p 5432:5432 postgres:16` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Snowflake Resource Monitor DDL
```sql
CREATE RESOURCE MONITOR quarterly_budget WITH
    CREDIT_QUOTA = 500
    FREQUENCY = 'QUARTERLY'
    START_TIMESTAMP = IMMEDIATELY
    TRIGGERS 
        ON 75 PERCENT DO NOTIFY
        ON 90 PERCENT DO NOTIFY
        ON 100 PERCENT DO SUSPEND
        ON 110 PERCENT DO SUSPEND_IMMEDIATE;
```

## Related Lessons
- Prerequisites: [[DW-05 - Partitioning and Clustering]]
- Next Lesson: [[LAK-01 - Object Storage Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
