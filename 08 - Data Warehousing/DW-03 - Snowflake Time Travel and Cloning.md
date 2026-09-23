---
id: DW-03
title: Snowflake Time Travel and Cloning
phase: Phase 2
module: Module 08: Data Warehousing Fundamentals
aliases:
  - DW-03
---

# DW-03 - Snowflake Time Travel and Cloning

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Utilize Snowflake Time Travel, Fail-Safe, and Zero-Copy Cloning for instant disaster recovery and isolated dev/test environments.

## Concepts
- **Time Travel Mechanics**: Accessing historical data at or before a specific timestamp or query ID (`AT(TIMESTAMP => ...)`, `BEFORE(STATEMENT => ...)`).
- **Data Retention Period**: 0 to 90 days configurable per table or database.
- **Fail-Safe**: Non-configurable 7-day disaster recovery period managed exclusively by Snowflake support for hardware disaster recovery.
- **Zero-Copy Cloning (`CLONE`)**: Creating an instant duplicate database, schema, or table without copying physical micro-partitions (copies only metadata pointers). Changes to clone create new copy-on-write partitions.

## Learning Resource
- **Title**: Snowflake Official Documentation - Understanding Time Travel and Cloning
- **Provider / Author**: Snowflake Inc.
- **URL**: https://docs.snowflake.com/en/user-guide/data-time-travel
- **Type**: Official Documentation
- **Topic**: Time Travel, Zero-Copy Cloning, Fail-Safe
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write SQL restoring an accidentally dropped table using `UNDROP TABLE`.
- [ ] Write a time-travel query fetching data as of 30 minutes prior to a bad batch update.
- [ ] Create a zero-copy clone of a production database for local testing: `CREATE DATABASE dev_test CLONE prod_db;`.

## Completion Criteria
- [ ] Explain how zero-copy cloning incurs zero initial storage cost.
- [ ] Reconstruct a corrupted table using Time Travel syntax.
- [ ] Differentiate between Time Travel and Fail-Safe.

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
### Time Travel Query Syntax
```sql
-- Query table exactly as it existed before a specific statement executed
SELECT * 
FROM orders 
BEFORE (STATEMENT => '8e6d0a79-0001-2f34-0000-00001234abcd');
```

## Related Lessons
- Prerequisites: [[DW-02 - Snowflake Architecture]]
- Next Lesson: [[DW-04 - Google BigQuery Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
