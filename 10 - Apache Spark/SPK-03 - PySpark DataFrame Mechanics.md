---
id: SPK-03
title: PySpark DataFrame Mechanics
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-03
---

# SPK-03 - PySpark DataFrame Mechanics

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master the PySpark DataFrame API: lazy transformations vs actions, schema definitions, column expressions, and partitioned writes.

## Concepts
- **Transformations vs Actions**:
  - *Transformations (Lazy)*: `select()`, `filter()`, `withColumn()`, `groupBy()`, `join()`. Build the execution plan without processing data.
  - *Actions (Eager)*: `show()`, `count()`, `collect()`, `write()`. Trigger physical DAG computation and job submission.
- **Narrow vs Wide Dependencies**:
  - *Narrow*: Each partition of parent RDD is used by at most one child partition (`map`, `filter`). Zero shuffle required.
  - *Wide*: Multiple child partitions depend on data from parent partitions (`groupBy`, `join`, `distinct`). Requires network shuffle across executors.
- **Explicit Schema Enforcement**: Using `StructType` and `StructField` to avoid costly schema inference scans.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 3: Apache Spark's Structured APIs
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: PySpark DataFrame API, Actions, Transformations
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Define an explicit `StructType` schema for a financial transactions dataset.
- [ ] Load a multi-million row dataset lazily, apply narrow filter and column transformations, and observe that no Spark job runs until an action is invoked.
- [ ] Write the transformed DataFrame to Parquet partitioned by `date` and bucketed by `account_id`.

## Completion Criteria
- [ ] Differentiate between narrow and wide transformations.
- [ ] Enforce strict schemas using `StructType` without runtime type inference.
- [ ] Explain why calling `.collect()` on large datasets causes Driver out-of-memory crashes.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | DataFrame programming | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Explicit Schema Pattern
```python
from pyspark.sql.types import StructType, StructField, StringType, DoubleType, TimestampType

schema = StructType([
    StructField("txn_id", StringType(), False),
    StructField("amount", DoubleType(), False),
    StructField("created_at", TimestampType(), True)
])
df = spark.read.schema(schema).parquet("s3://bucket/raw/")
```

## Related Lessons
- Prerequisites: [[SPK-01 - Spark 4 Cluster Architecture]]
- Next Lesson: [[SPK-04 - Catalyst Optimizer Deep Dive]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
