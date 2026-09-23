---
id: SPK-05
title: Spark SQL Internals
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-05
---

# SPK-05 - Spark SQL Internals

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master Spark SQL execution, temporary views, User-Defined Functions (UDFs), and vectorized Pandas UDFs (Arrow-optimized).

## Concepts
- **Spark SQL Engine**: Native ANSI SQL parser converting SQL text directly into Catalyst logical plan trees (identical performance to DataFrame API).
- **Temporary Views vs Managed Tables**: `createOrReplaceTempView()` (session-scoped) vs `saveAsTable()` (persistent catalog entry).
- **The Python UDF Performance Trap**: Standard Python UDFs (`@udf`) serialize row-by-row data between JVM and Python worker, destroying performance and disabling Catalyst optimizations.
- **Vectorized Pandas UDFs (PyArrow)**: `@pandas_udf` transfers entire Arrow RecordBatches to Python workers, executing vectorized operations at native C speed.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 5: Spark SQL and User-Defined Functions
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: Spark SQL, Pandas UDFs, Vectorization
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Register a DataFrame as a temporary SQL view and query it using `spark.sql()`.
- [ ] Implement a custom calculation using both a standard Python `@udf` and a vectorized `@pandas_udf`.
- [ ] Benchmark execution time across 5M rows to observe the dramatic performance advantage of Arrow-backed Pandas UDFs.

## Completion Criteria
- [ ] Explain why standard Python UDFs degrade Spark execution performance.
- [ ] Implement a vectorized Pandas UDF using PyArrow Apache Arrow serialization.
- [ ] Query Spark tables using native SQL syntax seamlessly alongside DataFrame API calls.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark & PyArrow | Vectorized UDF testing | Yes | Yes | `uv pip install pyspark pyarrow pandas` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Vectorized Pandas UDF Pattern
```python
import pandas as pd
from pyspark.sql.functions import pandas_udf
from pyspark.sql.types import DoubleType

@pandas_udf(DoubleType())
def calculate_tax(amounts: pd.Series) -> pd.Series:
    # Vectorized computation in C/Pandas directly over Arrow chunks
    return amounts * 0.0825
```

## Related Lessons
- Prerequisites: [[SPK-04 - Catalyst Optimizer Deep Dive]]
- Next Lesson: [[SPK-06 - Shuffling Mechanics]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
