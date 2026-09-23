---
id: DBT-03
title: dbt Core Setup and Architecture
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-03
---

# DBT-03 - dbt Core Setup and Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Initialize, configure, and structure production dbt-core projects with environment profiles and connection security.

## Concepts
- **dbt Project Anatomy**: `dbt_project.yml` (project configuration, model paths, materializations), `models/`, `seeds/`, `tests/`, `snapshots/`, `macros/`.
- **Profiles Configuration (`profiles.yml`)**: Managing database credentials, targets (dev, prod), threads, and isolating sensitive credentials outside the git repo (`~/.dbt/profiles.yml`).
- **The Jinja Compilation Engine**: Compiling modular `SELECT` statements into executable target database DDL (`CREATE VIEW AS`, `CREATE TABLE AS`).
- **The `ref()` and `source()` Functions**: Establishing automated lineage graphs (DAGs) and dynamic table references.

## Learning Resource
- **Title**: dbt Core Official Documentation & Best Practices Guide
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/docs/introduction
- **Type**: Official Documentation
- **Topic**: dbt-core, Project Setup, Profiles
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Initialize a new dbt project: `dbt init dbt_retail` using the DuckDB adapter.
- [ ] Configure `profiles.yml` with paths to your local DuckDB database file.
- [ ] Verify database connection and configuration using `dbt debug`.

## Completion Criteria
- [ ] Run `dbt debug` with all connection checks passing cleanly.
- [ ] Explain why database passwords and credentials must never be committed to git in `profiles.yml`.
- [ ] Understand the role of `ref()` in building dbt's dependency DAG.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Data build tool | Yes | Yes | `uv pip install dbt-core dbt-duckdb` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### profiles.yml for DuckDB
```yaml
dbt_retail:
  target: dev
  outputs:
    dev:
      type: duckdb
      path: 'warehouse.duckdb'
      threads: 4
```

## Related Lessons
- Prerequisites: [[DBT-02 - Embedded Analytics with DuckDB]]
- Next Lesson: [[DBT-04 - dbt Modeling Layers]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
