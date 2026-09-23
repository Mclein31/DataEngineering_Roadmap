---
id: LAK-08
title: Open Table Catalogs
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-08
---

# LAK-08 - Open Table Catalogs

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Deploy and evaluate modern Iceberg table catalogs: Apache Polaris, Project Nessie, AWS Glue Catalog, and Iceberg REST Catalog.

## Concepts
- **The Role of the Catalog in Iceberg**: Providing atomic pointer updates (CAS) for current metadata JSON and tracking namespace hierarchies (`database.table`).
- **Catalog Types**:
  - **Iceberg REST Catalog**: The open standard specification defining HTTP endpoints for metadata resolution, supported by all major compute engines.
  - **Apache Polaris**: Open-source cross-cloud REST catalog with centralized RBAC and multi-engine credential vending.
  - **Project Nessie**: Git-like version control for data lakes (`branch`, `tag`, `merge` whole data repositories).
  - **AWS Glue Data Catalog**: Native AWS cloud catalog supporting Iceberg table pointers.

## Learning Resource
- **Title**: Apache Iceberg REST Catalog Specification & Polaris Docs
- **Provider / Author**: Apache Software Foundation
- **URL**: https://iceberg.apache.org/concepts/catalog/
- **Type**: Official Documentation
- **Topic**: Iceberg Catalogs, REST Catalog, Polaris
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Deploy an open-source Iceberg REST catalog container via Docker Compose.
- [ ] Configure PySpark and DuckDB to connect to the local REST catalog.
- [ ] Create an Iceberg table from PySpark and immediately query it from DuckDB through the shared REST catalog.

## Completion Criteria
- [ ] Deploy a working Iceberg REST Catalog locally via Docker.
- [ ] Query the same Iceberg table from two different compute engines (PySpark and DuckDB) through the catalog.
- [ ] Explain why the Iceberg REST Catalog replaced engine-specific catalog implementations.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker & Iceberg REST Catalog | Catalog management | Yes | Yes | `Docker image tabulario/iceberg-rest` | https://iceberg.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Direct Parquet/Iceberg querying | Yes | Yes | `brew install duckdb` |

## Notes
### REST Catalog Configuration in PySpark
```python
spark = (
    SparkSession.builder
    .config("spark.sql.catalog.lake", "org.apache.iceberg.spark.SparkCatalog")
    .config("spark.sql.catalog.lake.type", "rest")
    .config("spark.sql.catalog.lake.uri", "http://localhost:8181")
    .getOrCreate()
)
```

## Related Lessons
- Prerequisites: [[LAK-05 - Apache Iceberg Architecture]]
- Next Lesson: [[SPK-01 - Spark 4 Cluster Architecture]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
