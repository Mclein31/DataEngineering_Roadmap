---
id: DAT-02
title: Pipeline Testing with Soda Core
phase: Phase 4
module: Module 15: Data Reliability Engineering & Observability
aliases:
  - DAT-02
---

# DAT-02 - Pipeline Testing with Soda Core

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Enforce declarative data quality contracts and execute automated data reliability checks using Soda Core (SodaCL).

## Concepts
- **Soda Core Architecture**: Open-source CLI and Python library translating declarative YAML data quality checks (SodaCL) into SQL assertions against databases and engines.
- **SodaCL (Soda Checks Language)**: Human-readable syntax for defining assertions:
  - Missing and validity checks: `missing_count(email) = 0`.
  - Anomaly detection: `row_count must be between 1000 and 50000`.
  - Schema drift assertions: `schema must match exactly [...]`.
- **Integration in Pipelines**: Running `soda scan` as an automated gate in Python extractors, Airflow tasks, or GitHub Actions CI.

## Learning Resource
- **Title**: Soda Core Official Documentation & SodaCL Guide
- **Provider / Author**: Soda Data Inc.
- **URL**: https://docs.soda.io/
- **Type**: Official Documentation
- **Topic**: Soda Core, SodaCL, Data Quality Gating
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install Soda Core for PostgreSQL and DuckDB: `uv pip install soda-core-postgres soda-core-duckdb`.
- [ ] Create a `checks.yml` file defining freshness, row count bounds, and column format assertions.
- [ ] Execute `soda scan -d my_datasource -c configuration.yml checks.yml` and inspect check results.

## Completion Criteria
- [ ] Write declarative data quality checks in SodaCL syntax.
- [ ] Execute a programmatic Soda scan inside a Python pipeline script.
- [ ] Halt pipeline execution if a critical Soda check encounters a failure.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Soda Core | Data quality testing | Yes | Yes | `uv pip install soda-core-postgres soda-core-duckdb` | https://docs.soda.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### SodaCL Checks Example (`checks.yml`)
```yaml
checks for fct_orders:
  - row_count > 0
  - missing_count(order_id) = 0
  - duplicate_count(order_id) = 0
  - freshness(order_created_at) < 24h
  - avg(total_amount) between 10 and 500
```

## Related Lessons
- Prerequisites: [[DAT-01 - The 5 Pillars of Observability]]
- Next Lesson: [[DAT-03 - Validation with Great Expectations]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
