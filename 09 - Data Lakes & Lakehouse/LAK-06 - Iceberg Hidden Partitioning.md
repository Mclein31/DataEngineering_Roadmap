---
id: LAK-06
title: Iceberg Hidden Partitioning
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-06
---

# LAK-06 - Iceberg Hidden Partitioning

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand how Iceberg Hidden Partitioning and Partition Evolution eliminate user query errors and avoid full table rewrites.

## Concepts
- **The Legacy Partitioning Trap**: In Hive, users had to know physical partition columns (`WHERE year = 2026 AND month = 9 AND ts >= '2026-09-23'`). Omitting the partition columns scanned the entire table!
- **Hidden Partitioning**: Iceberg tracks partition transformations (`year(ts)`, `month(ts)`, `day(ts)`, `bucket(16, id)`, `truncate(4, name)`) natively in metadata. Users query natural business fields (`WHERE ts >= '2026-09-23'`), and Iceberg automatically prunes partitions!
- **Partition Evolution**: Changing partition schemes (e.g., from `month(ts)` to `day(ts)`) without rewriting historical data files. Old data is read with old partition spec; new data is written with new spec.

## Learning Resource
- **Title**: Apache Iceberg: The Definitive Guide (Chapter 4: Hidden Partitioning)
- **Provider / Author**: Tomer Shiran, Jason Hughes, Alex Merced
- **URL**: https://www.dremio.com/resources/guides/apache-iceberg-the-definitive-guide/
- **Type**: Free Official eBook
- **Topic**: Hidden Partitioning, Partition Evolution
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create an Iceberg table partitioned by `month(order_date)`.
- [ ] Write a query filtering on `order_date BETWEEN '2026-09-01' AND '2026-09-15'` and observe partition pruning in the query plan.
- [ ] Evolve partition spec to `day(order_date)` and verify that old files remain valid without rewrite.

## Completion Criteria
- [ ] Explain why hidden partitioning prevents silent full-table scans.
- [ ] Implement partition evolution on an active Iceberg table.
- [ ] Use transform functions (`bucket`, `truncate`, `month`) in table DDL.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker / MinIO | Local object storage & service container | Yes | Yes | `brew install --cask docker` | https://min.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Direct Parquet/Iceberg querying | Yes | Yes | `brew install duckdb` |

## Notes
### Hidden Partition DDL Example
```sql
CREATE TABLE local.retail.orders (
    order_id STRING,
    customer_id BIGINT,
    order_ts TIMESTAMP,
    amount DECIMAL(10, 2)
)
USING iceberg
PARTITIONED BY (month(order_ts), bucket(16, customer_id));
```

## Related Lessons
- Prerequisites: [[LAK-05 - Apache Iceberg Architecture]]
- Next Lesson: [[LAK-07 - Delta Lake and UniForm]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
