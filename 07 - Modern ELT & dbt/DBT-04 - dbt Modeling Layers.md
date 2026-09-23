---
id: DBT-04
title: dbt Modeling Layers
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-04
---

# DBT-04 - dbt Modeling Layers

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Structure dbt transformation models into clear architectural layers: Staging, Intermediate, and Marts.

## Concepts
- **Staging Layer (`models/staging/`)**:
  - 1:1 relationship with raw source tables.
  - Cleansing only: renaming columns to snake_case, casting data types, initial filtering. No joins or business aggregations.
- **Intermediate Layer (`models/intermediate/`)**:
  - Complex business logic, joining multiple staging views together, sessionization, window calculations.
- **Marts Layer (`models/marts/`)**:
  - Final consumable reporting tables organized by business area (finance, marketing).
  - Modeled as Kimball Fact and Dimension tables.

## Learning Resource
- **Title**: dbt Best Practices: How we structure our dbt projects
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/best-practices/how-we-structure/1-guide-overview
- **Type**: Official Guide
- **Topic**: Project Structure, Staging, Intermediate, Marts
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create staging models `stg_orders.sql` and `stg_customers.sql` with column casting and alias cleaning.
- [ ] Create an intermediate model `int_customer_orders_aggregated.sql` joining orders and customers.
- [ ] Create a mart table `fct_orders.sql` and compile the project using `dbt compile`.

## Completion Criteria
- [ ] Strictly adhere to layer boundaries (zero joins in staging).
- [ ] Use `source()` macros to reference raw sources in staging models.
- [ ] Use `ref()` macros to reference upstream models in intermediate and mart layers.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Modeling layers | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Staging Model Pattern
```sql
-- models/staging/stg_orders.sql
with source as (
    select * from {{ source('retail', 'raw_orders') }}
),
renamed as (
    select
        id as order_id,
        customer_id,
        total_amount::numeric(10, 2) as order_amount,
        created_at::timestamp as order_created_at
    from source
)
select * from renamed
```

## Related Lessons
- Prerequisites: [[DBT-03 - dbt Core Setup and Architecture]]
- Next Lesson: [[DBT-05 - dbt Materializations]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
