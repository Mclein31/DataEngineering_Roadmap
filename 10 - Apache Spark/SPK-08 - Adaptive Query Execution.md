---
id: SPK-08
title: Adaptive Query Execution
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-08
---

# SPK-08 - Adaptive Query Execution

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Leverage Adaptive Query Execution (AQE) to dynamically re-optimize Spark query physical plans based on runtime shuffle statistics.

## Concepts
- **The Static Planning Problem**: Traditional cost-based optimizers rely on stale pre-query table statistics, frequently choosing suboptimal join strategies.
- **Adaptive Query Execution (AQE)**: Re-plans query execution dynamically between shuffle stages using actual runtime partition statistics.
- **Core AQE Capabilities**:
  - *Dynamically Coalescing Shuffle Partitions*: Merging hundreds of tiny post-shuffle partitions into optimal sizes (target 64MB) to prevent scheduler overhead.
  - *Dynamically Converting Sort-Merge Join to Broadcast Join*: If runtime filtering reduces a table below broadcast threshold, AQE converts SMJ to BHJ on the fly!
  - *Dynamically Mitigating Data Skew*: Automatically detecting oversized skewed partitions and splitting them into smaller balanced sub-tasks.

## Learning Resource
- **Title**: Apache Spark Documentation - Adaptive Query Execution
- **Provider / Author**: Apache Software Foundation
- **URL**: https://spark.apache.org/docs/latest/sql-performance-tuning.html#adaptive-query-execution
- **Type**: Official Documentation
- **Topic**: Adaptive Query Execution (AQE), Dynamic Optimization
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Verify AQE configuration: `spark.conf.get("spark.sql.adaptive.enabled")` (defaults to true in Spark 3.2+ and 4.0).
- [ ] Run a query with an aggressive filter and observe AQE dynamically converting a Sort-Merge Join to a Broadcast Hash Join in the Spark UI.
- [ ] Inspect the Spark UI DAG to observe dynamically coalesced shuffle partitions.

## Completion Criteria
- [ ] Explain the three core runtime optimizations performed by AQE.
- [ ] Identify dynamic join strategy changes in the Spark UI execution DAG.
- [ ] Configure `spark.sql.adaptive.advisoryPartitionSizeInBytes` to tune target partition size.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | AQE inspection | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### AQE Configuration Flags
```python
spark.conf.set("spark.sql.adaptive.enabled", "true")
spark.conf.set("spark.sql.adaptive.coalescePartitions.enabled", "true")
spark.conf.set("spark.sql.adaptive.autoBroadcastJoinThreshold", "20971520") # 20MB
spark.conf.set("spark.sql.adaptive.skewJoin.enabled", "true")
```

## Related Lessons
- Prerequisites: [[SPK-07 - Join Strategies in Spark]]
- Next Lesson: [[SPK-09 - Spark Unified Memory Management]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
