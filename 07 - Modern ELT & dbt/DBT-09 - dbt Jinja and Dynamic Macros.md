---
id: DBT-09
title: dbt Jinja and Dynamic Macros
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-09
---

# DBT-09 - dbt Jinja and Dynamic Macros

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Eliminate repetitive boilerplate SQL using Jinja templating, control flow, loops, and dynamic reusable dbt macros.

## Concepts
- **Jinja Templating in dbt**: Delimiters: `{% ... %}` (control flow, loops), `{{ ... }}` (expressions and print), `{# ... #}` (comments).
- **Macro Architecture (`macros/`)**: Reusable functions taking arguments and returning dynamic SQL snippets (equivalent to Python functions returning SQL).
- **Automated Pivoting with Jinja**: Dynamically looping through a list of values to generate pivot columns without hardcoding.
- **Cross-Database Adaptability**: Writing macros that execute database-specific SQL based on the target engine (`target.name` or adapter checks).

## Learning Resource
- **Title**: dbt Jinja & Macros Official Guide
- **Provider / Author**: dbt Labs
- **URL**: https://docs.getdbt.com/docs/build/jinja-macros
- **Type**: Official Documentation
- **Topic**: Jinja, Macros, Dynamic SQL
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write a macro `cents_to_dollars(column_name, decimal_places=2)` in `macros/cents_to_dollars.sql`.
- [ ] Use the macro across multiple models to convert integer payment amounts into formatted dollars.
- [ ] Write a Jinja loop in a model that pivots 10 payment methods into discrete column sums.

## Completion Criteria
- [ ] Create and test a custom dbt macro.
- [ ] Generate dynamic SQL using Jinja `{% for %}` loops.
- [ ] Inspect compiled SQL in `target/compiled/` to verify macro expansion.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Macro development | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Dynamic Pivot Macro
```sql
{% set payment_methods = ['credit_card', 'coupon', 'bank_transfer', 'gift_card'] %}

select
    order_id,
    {% for method in payment_methods %}
    sum(case when payment_method = '{{ method }}' then amount else 0 end) as {{ method }}_amount
    {% if not loop.last %},{% endif %}
    {% endfor %}
from {{ ref('stg_payments') }}
group by order_id
```

## Related Lessons
- Prerequisites: [[DBT-04 - dbt Modeling Layers]]
- Next Lesson: [[DBT-10 - dbt Documentation and Lineage]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
