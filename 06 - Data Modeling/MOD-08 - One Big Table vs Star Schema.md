---
id: MOD-08
title: One Big Table vs Star Schema
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-08
---

# MOD-08 - One Big Table vs Star Schema

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Evaluate the architectural tradeoffs between Kimball Star Schemas and One Big Table (OBT) in modern cloud data warehouses.

## Concepts
- **The One Big Table (OBT) Paradigm**: Denormalizing fact and all dimension attributes into a single massive, wide table (50–200 columns).
- **Why Cloud Warehouses Changed the Rules**:
  - In traditional row databases, OBT causes severe disk bloat and slow scans.
  - In columnar cloud warehouses (BigQuery, Snowflake, ClickHouse), columnar pruning means queries only read the columns requested, nulls compress for free, and join overhead is completely eliminated.
- **Trade-Off Analysis**:
  - *Star Schema Advantages*: Cleaner governance, modular maintenance, single point of update for dimensions, intuitive business model.
  - *OBT Advantages*: Highest BI dashboard performance, zero join latency, simplified SQL for analysts.
- **Hybrid Best Practice**: Modeling business logic as a Kimball Star Schema in dbt, then compiling pre-joined OBT views/marts for BI serving.

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 8: Serving Data for Analytics)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: OBT, Star Schema Tradeoffs, Columnar Engines
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Benchmark an analytical dashboard query on a 10M row dataset in DuckDB comparing a 4-table Star Schema join vs a pre-joined One Big Table.
- [ ] Measure runtime difference and memory usage between both approaches.

## Completion Criteria
- [ ] Articulate when OBT outperforms Star Schema and when Star Schema is mandatory for data governance.
- [ ] Explain how columnar compression makes wide OBT tables economical in cloud warehouses.
- [ ] Design a dbt mart model that compiles a Star Schema into an OBT serving view.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Benchmarking joins vs OBT | Yes | Yes | `brew install duckdb` | https://duckdb.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Modern Hybrid Pattern
```text
Staging (Cleaned Source) 
    ↓
Dimensional Core (Kimball Star Schema: facts & dims) ──> Enterprise Governance
    ↓
Serving Layer (Compiled One Big Table / Wide Views)  ──> BI Dashboards
```

## Related Lessons
- Prerequisites: [[MOD-02 - Kimball Dimensional Modeling]]
- Next Lesson: [[DBT-01 - Modern ELT Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
