---
id: DBT-08
title: Advanced Testing and Expectations
phase: Phase 2
module: Module 07: Modern In-Warehouse ELT & dbt
aliases:
  - DBT-08
---

# DBT-08 - Advanced Testing and Expectations

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Integrate advanced data testing packages (`dbt_expectations`) to enforce statistical bounds, distribution checks, and string regex assertions.

## Concepts
- **Package Management in dbt (`packages.yml`)**: Installing community packages (`dbt-labs/dbt_utils`, `calogica/dbt_expectations`).
- **`dbt_expectations`**: Porting Great Expectations concepts directly into dbt:
  - Column value ranges (`expect_column_values_to_be_between`).
  - Distribution and proportion tests (`expect_column_proportion_of_unique_values_to_be_between`).
  - Regex pattern matching (`expect_column_values_to_match_regex`).
- **Freshness Assertions (`dbt source freshness`)**: Asserting source tables have loaded new data within defined SLA thresholds (`warn_after`, `error_after`).

## Learning Resource
- **Title**: dbt-expectations Package Documentation
- **Provider / Author**: Calogica / dbt Labs
- **URL**: https://github.com/calogica/dbt-expectations
- **Type**: Open-Source Package
- **Topic**: Statistical Quality Testing, dbt Packages
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a `packages.yml` file and add `dbt_utils` and `dbt_expectations`.
- [ ] Run `dbt deps` to install package dependencies.
- [ ] Configure an expectation asserting that order discount percentage never exceeds 0.50 (50%).
- [ ] Configure `freshness` block on source tables and run `dbt source freshness`.

## Completion Criteria
- [ ] Successfully install and run tests from `dbt_expectations`.
- [ ] Validate source data arrival SLAs using `dbt source freshness`.
- [ ] Catch an intentional out-of-bounds anomaly with a statistical expectation test.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| dbt-core | Package testing | Yes | Yes | `uv pip install dbt-core` | https://docs.getdbt.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### packages.yml
```yaml
packages:
  - package: dbt-labs/dbt_utils
    version: 1.1.1
  - package: calogica/dbt_expectations
    version: 0.10.1
```

## Related Lessons
- Prerequisites: [[DBT-07 - dbt Testing Framework]]
- Next Lesson: [[DBT-09 - dbt Jinja and Dynamic Macros]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
