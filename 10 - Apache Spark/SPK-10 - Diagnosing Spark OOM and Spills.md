---
id: SPK-10
title: Diagnosing Spark OOM and Spills
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-10
---

# SPK-10 - Diagnosing Spark OOM and Spills

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Diagnose, triage, and eliminate Spark driver and executor OutOfMemoryError crashes and disk spills under production workloads.

## Concepts
- **Types of Spark OOM Errors**:
  - *Driver OOM (`java.lang.OutOfMemoryError: Java heap space`)*: Caused by calling `.collect()` or `toPandas()` on huge datasets, or broadcasting oversized tables.
  - *Executor OOM*: Individual task partition exceeds execution memory pool during wide shuffles or Cartesian joins.
  - *Container Killed by YARN/K8s (`Exit Code 137`)*: Off-heap memory overhead exceeded (`spark.executor.memoryOverhead`), often caused by PyArrow or Python workers.
- **Diagnosing Spills**: Distinguishing "Spill (Memory)" (uncompressed size in RAM) from "Spill (Disk)" (compressed size on local disk).
- **Remediation Techniques**: Increasing shuffle partitions, salting join keys, allocating sufficient `memoryOverhead`.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Tuning and Troubleshooting
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: OutOfMemoryError, Memory Spills, Exit Code 137
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Intentionally cause a Driver OOM by creating a 10M row DataFrame and calling `.collect()`.
- [ ] Inspect executor task details in Spark UI to identify tasks with high `Spill (Memory)` and `Spill (Disk)`.
- [ ] Reconfigure shuffle partitions and executor memory to eliminate disk spill completely.

## Completion Criteria
- [ ] Articulate the root causes of Driver OOM vs Executor OOM.
- [ ] Explain what causes container exit code 137 and how to fix it via `spark.executor.memoryOverhead`.
- [ ] Eliminate shuffle disk spill in a benchmark query.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Troubleshooting OOM | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Troubleshooting OOM Matrix
| Symptom | Root Cause | Fix |
| :--- | :--- | :--- |
| Driver OOM | `.collect()` on large DataFrame | Write to storage; use `.take(100)` |
| Executor OOM | Partition too large for task | Increase shuffle partitions |
| Exit Code 137 | Off-heap memory exceeded by PyArrow | Increase `spark.executor.memoryOverhead` |

## Related Lessons
- Prerequisites: [[SPK-09 - Spark Unified Memory Management]]
- Next Lesson: [[SPK-11 - Data Skew Mitigation]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
