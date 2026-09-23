---
certification: Databricks Certified Data Engineer Associate
provider: Databricks
current_status: ACTIVE
exam: Databricks Certified Data Engineer Associate
cost: 200 USD
aliases:
  - Databricks Certified Data Engineer Associate
---

# 🧱 Databricks Certified Data Engineer Associate

## Overview
The Databricks Certified Data Engineer Associate exam validates proficiency in using the Databricks Lakehouse platform to complete foundational data engineering tasks, including PySpark processing, Delta Lake table management, pipeline automation with Delta Live Tables, and data governance with Unity Catalog.

---

## 📋 Exam Specification
- **Certification**: Databricks Certified Data Engineer Associate
- **Provider**: Databricks
- **Current Status**: **ACTIVE**
- **Exam Code**: Databricks Certified Data Engineer Associate
- **Prerequisites**: None official (Proficiency in Python, SQL, and Apache Spark)
- **Recommended Experience**: 6 months hands-on experience on the Databricks Lakehouse Platform
- **Cost**: $200 USD
- **Exam Format**: 45 multiple-choice questions
- **Duration**: 90 minutes
- **Passing Score**: 70%
- **Renewal / Validity**: 2 years
- **Official URL**: [databricks.com/learn/certification/data-engineer-associate](https://www.databricks.com/learn/certification/data-engineer-associate)

---

## 📊 Exam Domains & Weightings

```text
Domain 1: Databricks Platform Architecture & Workspace (24%)
Domain 2: Data Ingestion with Auto Loader and COPY INTO (26%)
Domain 3: Data Processing with PySpark & Spark SQL (26%)
Domain 4: Data Pipelines with Delta Live Tables & Unity Catalog (24%)
```

### Domain 1: Databricks Lakehouse Platform (24%)
- Control plane vs data plane architecture.
- Cluster configuration: Single-node vs multi-node, worker sizing, driver memory, auto-scaling.
- Databricks Repos: Git integration, branch synchronization.

### Domain 2: Data Ingestion (26%)
- Auto Loader: Directory watching vs file notification mode, schema inference, schema evolution (`mergeSchema`, `rescueServer`).
- `COPY INTO`: Idempotent file loading, comparing `COPY INTO` vs Auto Loader for batch vs continuous ingestion.

### Domain 3: Data Processing (26%)
- Delta Lake ACID transactions, transaction log (`_delta_log`), time-travel syntax (`RESTORE`, `VERSION AS OF`).
- Optimizations: `OPTIMIZE` compaction, `Z-ORDER BY`, vacuuming tombstoned files (`VACUUM`).

### Domain 4: Data Pipelines & Governance (24%)
- Delta Live Tables (DLT): Streaming tables vs materialized views, expectations (`CONSTRAINT ... ON VIOLATION DROP ROW`).
- Unity Catalog: Three-level namespace (`catalog.schema.table`), grant permissions (`GRANT SELECT ON ...`).

---

## 🛠️ Free Preparation Resources
1. **Databricks Academy**: Free self-paced Data Engineer Learning Path for community members.
2. **Databricks Community Edition**: Free cloud sandbox with a micro-cluster for hands-on experimentation.
