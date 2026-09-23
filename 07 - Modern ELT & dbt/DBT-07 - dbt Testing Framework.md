---
id: DBT-07
title: dbt Testing Framework
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-07
---

# DBT-07 - dbt Testing Framework

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Enforce data quality gates using dbt generic schema tests and custom singular SQL assertions.

## Concepts
- **The 4 Out-of-the-Box Generic Schema Tests**:
  - `unique`: Verifies every value in a column is unique (no duplicates).
  - `not_null`: Asserts column contains zero NULL values.
  - `accepted_values`: Asserts column values belong to a discrete enumerated list (`values: ['COMPLETED', 'PENDING', 'CANCELLED']`).
  - `relationships`: Foreign key referential integrity test asserting foreign key values exist in parent table (`to: ref('dim_customers'), field: customer_id`).
- **Singular Tests (`tests/`)**: Custom SQL queries asserting business logic; test FAILS if the query returns any rows!
- **Severity Thresholds**: Configuring `warn` vs `error` and row thresholds to halt pipeline progression on critical bugs.

## Learning Resource
- **Title**: dbt Tests Documentation
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/docs/build/tests
- **Type**: Official Documentation
- **Topic**: Data Quality, Schema Testing, Singular Tests
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure `unique` and `not_null` assertions on primary keys in `schema.yml`.
- [ ] Add a `relationships` test asserting all `fct_orders.customer_id` records exist in `dim_customers`.
- [ ] Write a singular SQL test `assert_order_total_matches_line_items.sql` asserting total order amount equals sum of line items.

## Completion Criteria
- [ ] Configure and pass all 4 generic test types across staging and mart models.
- [ ] Write a custom singular SQL test asserting complex business logic.
- [ ] Execute `dbt test` and verify zero assertion failures.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Data quality testing | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Singular Test Example
```sql
-- tests/assert_positive_revenue.sql
-- FAILS if any row is returned
select
    order_id,
    order_amount
from {{ ref('fct_orders') }}
where order_amount < 0
```

## Related Lessons
- Prerequisites: [[DBT-04 - dbt Modeling Layers]]
- Next Lesson: [[DBT-08 - Advanced Testing and Expectations]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
