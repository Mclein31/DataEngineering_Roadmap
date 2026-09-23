---
id: SPK-09
title: Spark Unified Memory Management
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-09
---

# SPK-09 - Spark Unified Memory Management

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master JVM memory layout inside Spark executors: On-Heap vs Off-Heap, Execution Memory, Storage Memory, and User Memory.

## Concepts
- **Spark Executor Memory Layout**:
  - `Reserved Memory`: 300MB hardcoded for Spark internal system operations.
  - `Spark Memory Pool (default 60%)`: Shared dynamically between Execution and Storage.
    - *Execution Memory*: Used for shuffles, joins, sorts, aggregations.
    - *Storage Memory*: Used for cached DataFrames (`.persist()`, `.cache()`) and broadcast variables.
  - `User Memory (default 40%)`: Used for user data structures, metadata, and custom objects.
  - `Overhead Memory (default 10%)`: Off-heap memory for VM overhead, PySpark worker communication, and native C libraries.
- **Dynamic Borrowing**: Execution memory can borrow from Storage memory and evict cached partitions to disk if shuffle demands increase! Storage memory cannot evict execution memory.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 7: Memory Management
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: JVM Memory Pools, Execution vs Storage Memory
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Calculate exact executor memory pools for a worker allocated with `--executor-memory 8G`.
- [ ] Cache a DataFrame using `.persist(StorageLevel.MEMORY_AND_DISK)` and inspect memory utilization in the Spark UI "Storage" tab.
- [ ] Observe execution memory dynamically evicting cached partitions during a massive shuffle stage.

## Completion Criteria
- [ ] Calculate memory pool allocations across Execution, Storage, and User memory.
- [ ] Explain the dynamic eviction policy between Execution and Storage memory.
- [ ] Choose appropriate `StorageLevel` (e.g. `MEMORY_ONLY` vs `MEMORY_AND_DISK_SER`).

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Memory tuning | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Spark Executor Memory Diagram
```text
Total Executor Memory (e.g., 8GB)
  ├── Reserved Memory (300MB)
  └── Usable Memory:
        ├── Spark Memory Pool (60%):
        │     ├── Execution Memory (Sorts/Joins/Shuffles) <── Borrowing
        │     └── Storage Memory (Cached Tables/Broadcast) ──> Eviction
        └── User Memory (40%): User data structures, UDF memory
```

## Related Lessons
- Prerequisites: [[SPK-06 - Shuffling Mechanics]]
- Next Lesson: [[SPK-10 - Diagnosing Spark OOM and Spills]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
