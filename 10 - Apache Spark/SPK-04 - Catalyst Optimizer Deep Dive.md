---
id: SPK-04
title: Catalyst Optimizer Deep Dive
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-04
---

# SPK-04 - Catalyst Optimizer Deep Dive

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand how Spark's Catalyst Optimizer transforms DataFrame queries into highly optimized physical execution bytecode.

## Concepts
- **The 4 Catalyst Optimization Phases**:
  1. *Analysis*: Resolves table names and attribute types against the Catalog to produce an Analyzed Logical Plan.
  2. *Logical Optimization*: Rule-based optimizations (constant folding, predicate pushdown, projection pruning).
  3. *Physical Planning*: Generates multiple physical plans and selects the lowest-cost model using Cost-Based Optimization (CBO).
  4. *Code Generation (Tungsten)*: Compiles the physical plan into optimized Java bytecode (Whole-Stage Code Generation).
- **Inspecting Plans with `explain(mode='formatted')`**: Analyzing Parsed, Analyzed, Optimized, and Physical plans.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 3: Spark SQL and the Catalyst Optimizer
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: Catalyst Optimizer, Tungsten, Physical Plans
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write a PySpark query with filters placed after join operations.
- [ ] Execute `df.explain(True)` and verify that Catalyst automatically pushed the filter down before the join stage in the Optimized Logical Plan.
- [ ] Identify `*(1) WholeStageCodegen` markers in physical plan output.

## Completion Criteria
- [ ] Walk through the 4 phases of Catalyst optimization.
- [ ] Identify Predicate Pushdown and Column Pruning in an optimized plan.
- [ ] Explain how Whole-Stage Code Generation eliminates virtual function call overhead in JVM loops.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Query plan analysis | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Catalyst Optimizer Flow
```text
Unresolved Logical Plan ──[Analysis (Catalog)]──> Analyzed Logical Plan
                                                          ↓
                                              [Logical Optimization]
                                                          ↓
                                               Optimized Logical Plan
                                                          ↓
                                                [Physical Planning]
                                                          ↓
                                              Selected Physical Plan
                                                          ↓
                                            [Code Generation (Tungsten)]
                                                          ↓
                                                   Java Bytecode
```

## Related Lessons
- Prerequisites: [[SPK-03 - PySpark DataFrame Mechanics]]
- Next Lesson: [[SPK-05 - Spark SQL Internals]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
