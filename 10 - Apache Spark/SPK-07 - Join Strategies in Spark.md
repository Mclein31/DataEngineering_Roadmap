---
id: SPK-07
title: Join Strategies in Spark
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-07
---

# SPK-07 - Join Strategies in Spark

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master distributed join strategies in Spark: Broadcast Hash Join, Shuffle Hash Join, Sort-Merge Join, and Cartesian Join.

## Concepts
- **Broadcast Hash Join (BHJ)**:
  - Broadcasts the entire smaller table (default < 10MB, `spark.sql.autoBroadcastJoinThreshold`) to all executors.
  - Zero shuffle required; completely eliminates wide network redistribution.
- **Sort-Merge Join (SMJ)**:
  - Default for large-to-large joins. Both tables are hashed, shuffled across network into identical partitions, sorted by join key, and merged.
- **Shuffle Hash Join**: Hashing both sides without pre-sorting; optimal when one side is moderately smaller than the other.
- **Broadcast Nested Loop Join (BNLJ)**: Fallback for joins without equality conditions (`ON a.val > b.val`). Extremely slow; causes massive Cartesian products.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 7: Optimizing and Tuning Apache Spark
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: Join Strategies, Broadcast Join, Sort-Merge
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Join a 5M row fact table with a small 500-row dimension table in PySpark.
- [ ] Inspect physical plan with `df.explain()` to verify `BroadcastHashJoin`.
- [ ] Force a Broadcast Join on a larger table using `from pyspark.sql.functions import broadcast; df_large.join(broadcast(df_dim), "id")`.

## Completion Criteria
- [ ] Identify which join strategy Catalyst selects from the physical plan.
- [ ] Use `broadcast()` hint safely without causing driver OutOfMemoryError.
- [ ] Explain the memory and network trade-offs between Broadcast Hash Join and Sort-Merge Join.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Join tuning | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Join Strategy Selection Matrix
| Condition | Join Strategy | Shuffle Required? |
| :--- | :--- | :--- |
| One table < 10MB (or broadcast hint) | Broadcast Hash Join (BHJ) | **No** (Zero network shuffle) |
| Large tables with equality join | Sort-Merge Join (SMJ) | **Yes** (Full hash shuffle) |
| Non-equi join (`col1 > col2`) | Broadcast Nested Loop Join | **No** (High CPU Cartesian) |

## Related Lessons
- Prerequisites: [[SPK-06 - Shuffling Mechanics]]
- Next Lesson: [[SPK-08 - Adaptive Query Execution]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
