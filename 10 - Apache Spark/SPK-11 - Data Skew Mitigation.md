---
id: SPK-11
title: Data Skew Mitigation
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-11
---

# SPK-11 - Data Skew Mitigation

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Detect, analyze, and resolve data skew in distributed joins using key salting, isolated joins, and broadcast hints.

## Concepts
- **The Data Skew Phenomenon**: When data distribution on a join or group key is heavily uneven (e.g. 90% of rows have `customer_id = 1` or `NULL`).
- **The "Straggler Task" Problem**: 99 tasks finish in 5 seconds, but 1 task runs for 2 hours on the single overloaded executor holding the skewed key.
- **Key Salting Technique**: Appending random integer suffixes (`0..N`) to the skewed key on the large table and exploding the matching key on the dimension table to distribute skewed data across multiple executor cores.
- **Filtering / Isolating Null Keys**: Splitting null and dummy keys before the join and unioning afterwards.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 7: Mitigating Data Skew
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: Data Skew, Key Salting, Stragglers
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Synthesize a dataset where 80% of rows have `user_id = 9999`.
- [ ] Perform a Sort-Merge Join and observe the straggler task in Spark UI.
- [ ] Implement key salting with 5 salt buckets, re-run, and observe balanced task execution times across all executors.

## Completion Criteria
- [ ] Identify data skew in the Spark UI Task Distribution summary (max duration >> median duration).
- [ ] Implement key salting in PySpark to evenly distribute skewed keys.
- [ ] Compare query completion times before and after salting.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Skew mitigation | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Key Salting Implementation
```python
from pyspark.sql import functions as F

SALT_FACTOR = 4

# Salt the skewed table
df_skewed = df_skewed.withColumn("salt", F.concat(F.col("user_id"), F.lit("_"), F.floor(F.rand() * SALT_FACTOR)))

# Explode the lookup dimension table
df_dim_exploded = (
    df_dim
    .withColumn("salt_array", F.array([F.lit(i) for i in range(SALT_FACTOR)]))
    .withColumn("salt_idx", F.explode("salt_array"))
    .withColumn("salt", F.concat(F.col("user_id"), F.lit("_"), F.col("salt_idx")))
)

# Join on the salted key
result = df_skewed.join(df_dim_exploded, on="salt").drop("salt", "salt_array", "salt_idx")
```

## Related Lessons
- Prerequisites: [[SPK-07 - Join Strategies in Spark]]
- Next Lesson: [[SPK-12 - Spark Structured Streaming]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
