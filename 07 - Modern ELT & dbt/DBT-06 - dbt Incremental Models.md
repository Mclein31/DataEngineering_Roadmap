---
id: DBT-06
title: dbt Incremental Models
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-06
---

# DBT-06 - dbt Incremental Models

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build high-scale incremental dbt models processing only delta records to reduce warehouse compute and build times by > 90%.

## Concepts
- **The Incremental Problem**: Full table refreshes (`CREATE TABLE AS`) become computationally impossible as tables grow beyond gigabytes.
- **The `is_incremental()` Macro**: Conditional Jinja block filtering source records based on the latest watermark in the target table:
  `{% if is_incremental() %} where updated_at > (select max(updated_at) from {{ this }}) {% endif %}`.
- **Incremental Merge Strategies**:
  - `merge`: Performs an ACID SQL `MERGE` matching on `unique_key`, updating existing records and inserting new ones.
  - `append`: Appends new records without deduplication (ideal for immutable event streams).
  - `delete+insert`: Deletes matching keys in target before inserting delta batch.
- **The `--full-refresh` Flag**: Forcing a complete rebuild when schemas evolve or backfills occur.

## Learning Resource
- **Title**: dbt Incremental Models Deep Dive
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/docs/build/incremental-models
- **Type**: Official Documentation
- **Topic**: Incremental Modeling, Merge Strategies, Watermarking
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Build an incremental model `fct_orders_incremental.sql` using `unique_key='order_id'` and `strategy='merge'`.
- [ ] Implement watermark filtering using `is_incremental()` on `order_updated_at`.
- [ ] Run `dbt run --select fct_orders_incremental`, insert 5 mock delta rows into source, re-run, and verify that only the 5 rows were merged.

## Completion Criteria
- [ ] Implement an incremental model with `unique_key` and watermark filtering.
- [ ] Verify that incremental runs process only delta rows.
- [ ] Execute `dbt run --full-refresh` cleanly to rebuild the model from scratch.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Incremental modeling | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Production Incremental Model Pattern
```sql
{{ config(
    materialized = 'incremental',
    unique_key = 'order_id',
    incremental_strategy = 'merge'
) }}

select * from {{ ref('stg_orders') }}

{% if is_incremental() %}
  where order_updated_at > (select coalesce(max(order_updated_at), '1970-01-01') from {{ this }})
{% endif %}
```

## Related Lessons
- Prerequisites: [[DBT-05 - dbt Materializations]]
- Next Lesson: [[DBT-07 - dbt Testing Framework]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
