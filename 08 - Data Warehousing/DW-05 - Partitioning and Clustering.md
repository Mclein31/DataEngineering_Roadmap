---
id: DW-05
title: Partitioning and Clustering
phase: Phase 2
module: Module 08: Data Warehousing Fundamentals
aliases:
  - DW-05
---

# DW-05 - Partitioning and Clustering

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Optimize cloud warehouse query performance and slash query scan costs using physical partitioning and multi-column clustering.

## Concepts
- **Table Partitioning**: Physically dividing table data into discrete segments based on a low-cardinality key (e.g., date, ingestion timestamp, integer range).
- **Partition Pruning**: The query engine skips entire partition files if the query `WHERE` clause does not match the partition predicate, reducing bytes scanned by > 95%.
- **Table Clustering**: Colocating related data within partitions based on high-cardinality keys (`customer_id`, `product_id`).
- **Combining Partitioning and Clustering**: Best practice pattern: Partition by `order_date` and cluster by `(customer_id, country_code)`.

## Learning Resource
- **Title**: BigQuery Documentation - Introduction to Partitioned and Clustered Tables
- **Provider / Author**: Google Cloud
- **URL**: https://cloud.google.com/bigquery/docs/partitioned-tables
- **Type**: Official Documentation
- **Topic**: Partitioning, Clustering, Cost Optimization
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write SQL creating a partitioned and clustered table in BigQuery or Snowflake:
  `PARTITION BY DATE(created_at) CLUSTER BY customer_id, order_status`.
- [ ] Compare bytes scanned between a partitioned query vs an unpartitioned query over identical datasets.

## Completion Criteria
- [ ] Correctly choose partition keys (coarse-grained, e.g. Date) vs cluster keys (fine-grained, e.g. IDs).
- [ ] Explain how partition pruning directly reduces cloud query bills.
- [ ] Avoid the anti-pattern of over-partitioning on high-cardinality keys.

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
### BigQuery DDL Example
```sql
CREATE TABLE `project.analytics.fct_orders` (
    order_id STRING,
    customer_id INT64,
    order_date DATE,
    total_amount NUMERIC
)
PARTITION BY order_date
CLUSTER BY customer_id;
```

## Related Lessons
- Prerequisites: [[DW-04 - Google BigQuery Architecture]]
- Next Lesson: [[DW-06 - Warehouse Cost Governance]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
