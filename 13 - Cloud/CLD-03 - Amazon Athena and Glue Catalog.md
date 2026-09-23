---
id: CLD-03
title: Amazon Athena and Glue Catalog
phase: Phase 4
module: Module 13: Cloud Infrastructure (AWS Focus)
aliases:
  - CLD-03
---

# CLD-03 - Amazon Athena and Glue Catalog

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Query S3 data lakes serverlessly using Amazon Athena and manage metadata schemas with the AWS Glue Data Catalog.

## Concepts
- **AWS Glue Data Catalog**: Persistent central metadata repository compatible with Apache Hive metastore; stores database definitions, table schemas, and partition locations.
- **Amazon Athena Engine**: Serverless distributed query engine based on Presto/Trino; executes standard ANSI SQL directly against S3 data without server management.
- **Cost Model ($5.00 per TB Scanned)**: Why partitioning, columnar Parquet format, and Snappy/ZSTD compression are essential to prevent massive bills.
- **Partition Projection**: Eliminating Glue Catalog metadata bottleneck for high-partition tables by projecting partitions via configuration keys.

## Learning Resource
- **Title**: Amazon Athena User Guide - Performance Tuning
- **Provider / Author**: Amazon Web Services
- **URL**: https://docs.aws.amazon.com/athena/latest/ug/performance-tuning.html
- **Type**: Official Documentation
- **Topic**: Athena Serverless SQL, Glue Catalog, Partition Projection
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Register an external table in AWS Glue Data Catalog pointing to partitioned Parquet files in S3.
- [ ] Execute analytical queries in Amazon Athena filtering on partition columns.
- [ ] Calculate query cost: compare scanning a 100GB CSV vs a 5GB compressed Parquet file.

## Completion Criteria
- [ ] Register and partition a table in the AWS Glue Data Catalog.
- [ ] Execute an Athena query and verify partition pruning in the scanned byte metrics.
- [ ] Configure Athena Workgroups to enforce query data limits and cost guardrails.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AWS CLI / LocalStack | Athena & Glue testing | Yes | Yes | `brew install awscli` | https://aws.amazon.com/athena/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Athena External Table DDL
```sql
CREATE EXTERNAL TABLE IF NOT EXISTS glue_db.fct_orders (
    order_id STRING,
    customer_id BIGINT,
    amount DOUBLE
)
PARTITIONED BY (order_date STRING)
STORED AS PARQUET
LOCATION 's3://company-lakehouse-curated/orders/';
```

## Related Lessons
- Prerequisites: [[CLD-02 - Amazon S3 Storage Architecture]]
- Next Lesson: [[CLD-04 - Amazon EMR Serverless Spark]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
