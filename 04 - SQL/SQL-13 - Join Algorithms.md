---
id: SQL-13
title: Join Algorithms
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-13
---

# SQL-13 - Join Algorithms

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master the computational and memory tradeoffs of relational join engines: Nested Loop, Hash Join, and Sort-Merge Join.

## Concepts
- **Nested Loop Join**: Iterating outer rows and probing inner table per row. Highly optimal when outer set is small and inner table has indexed lookup.
- **Hash Join**:
  - *Build Phase*: Reads inner (smaller) table and builds in-memory hash table on join key.
  - *Probe Phase*: Scans outer table and probes hash table for matches.
  - *Batched / Disk Spill*: If hash table exceeds `work_mem`, spills partitions to temporary disk files.
- **Sort-Merge Join**: Both datasets sorted on join key, then merged in a single pass. Ideal for large sorted tables without requiring hash memory.

## Learning Resource
- **Title**: Use The Index, Luke! - Join Algorithms
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: Hash Join, Sort-Merge, Nested Loop
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Join two tables in PostgreSQL and observe planner join choice in `EXPLAIN ANALYZE`.
- [ ] Force the engine to evaluate different join algorithms by toggling planner flags:
  `SET enable_hashjoin = off;`, `SET enable_mergejoin = off;`, `SET enable_nestloop = off;`.
- [ ] Measure execution runtime differences across all three join algorithms for identical data.

## Completion Criteria
- [ ] Explain the time complexity and memory requirements of a Hash Join vs a Sort-Merge Join.
- [ ] Identify what causes a Hash Join to spill to disk (`Batches: > 1`).
- [ ] Force PostgreSQL to evaluate all 3 join strategies for a query using planner switches.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Relational testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community / pgAdmin | GUI database client | Yes | Yes | Free universal SQL client |

## Notes
### Join Trade-Off Comparison
| Algorithm | Best When | Time Complexity | Memory Requirements |
| :--- | :--- | :--- | :--- |
| **Nested Loop** | One table tiny, other has B-Tree index | $O(N \log M)$ | Minimal |
| **Hash Join** | Medium-to-large unsorted tables | $O(N + M)$ | Proportional to smaller table (`work_mem`) |
| **Sort-Merge** | Inputs already sorted on join key | $O(N \log N + M \log M)$ | Low if pre-sorted |

## Related Lessons
- Prerequisites: [[SQL-11 - Execution Plans with EXPLAIN]]
- Next Lesson: [[SQL-14 - Indexing Strategies and B-Trees]]
- Phase Overview: [[Phase 1 - Foundations]]
