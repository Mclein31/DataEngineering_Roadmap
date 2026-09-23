---
id: DBT-05
title: dbt Materializations
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-05
---

# DBT-05 - dbt Materializations

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master the 4 core dbt materialization strategies: View, Table, Incremental, and Ephemeral.

## Concepts
- **View Materialization (`materialized='view'`)**: Lightweight virtual query; fast build, zero storage cost, but re-computes query on every consumer read.
- **Table Materialization (`materialized='table'`)**: Drops and recreates a physical table on every run; fast for consumer queries, but expensive to build on large datasets.
- **Ephemeral Materialization (`materialized='ephemeral'`)**: Interpolates SQL into downstream models as a CTE; creates no database object.
- **Configuring Materializations**: Setting defaults in `dbt_project.yml` vs overriding per-model with `{{ config(materialized='table') }}`.

## Learning Resource
- **Title**: dbt Materializations Documentation
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/docs/build/materializations
- **Type**: Official Documentation
- **Topic**: Materializations, Views, Tables, Ephemeral
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure all staging models to materialize as `view` in `dbt_project.yml`.
- [ ] Configure intermediate models as `ephemeral` and mart models as `table`.
- [ ] Run `dbt run` and inspect the generated database schema to verify views vs physical tables.

## Completion Criteria
- [ ] Choose appropriate materializations based on query frequency, latency SLA, and table size.
- [ ] Configure materializations hierarchically in `dbt_project.yml`.
- [ ] Inspect compiled SQL in `target/compiled/` and `target/run/`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Materialization execution | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Configuration Syntax
```sql
{{ config(
    materialized = 'table',
    schema = 'marts'
) }}

select * from {{ ref('stg_orders') }}
```

## Related Lessons
- Prerequisites: [[DBT-04 - dbt Modeling Layers]]
- Next Lesson: [[DBT-06 - dbt Incremental Models]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
