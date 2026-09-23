---
id: MOD-05
title: Slowly Changing Dimensions
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-05
---

# MOD-05 - Slowly Changing Dimensions

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement Slowly Changing Dimension (SCD) strategies (Type 0 through Type 6) to preserve or overwrite historical attributes accurately.

## Concepts
- **The SCD Challenge**: How to handle changes to dimension attributes over time (e.g., customer moves from New York to Austin).
- **Core SCD Strategies**:
  - **Type 0 (Retain Original)**: Attribute never changes (e.g., original date of birth).
  - **Type 1 (Overwrite)**: Overwrite historical value with new value. Zero history preserved; historical facts are re-attributed to new value.
  - **Type 2 (Add New Row)**: Full history preservation. Creates a new row with new surrogate key, `valid_from`, `valid_to` (or `NULL`), and `is_current` boolean flag.
  - **Type 3 (Add New Column)**: Tracks previous value as a separate column (`current_city`, `previous_city`). Limited to 1 previous change.
  - **Type 4 (Historical Min-Dimension)**: Rapidly changing attributes moved to separate historical table.
  - **Type 6 (Hybrid 1 + 2 + 3)**: Combines Type 1, 2, and 3 capabilities.

## Learning Resource
- **Title**: The Data Warehouse Toolkit (Chapter 4: Slowly Changing Dimensions)
- **Provider / Author**: Ralph Kimball & Margy Ross (Wiley)
- **URL**: https://www.wiley.com/en-us/The+Data+Warehouse+Toolkit%3A+The+Definitive+Guide+to+Dimensional+Modeling%2C+3rd+Edition-p-9781118530801
- **Type**: Textbook
- **Topic**: Slowly Changing Dimensions (SCD 1-6)
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a `dim_customers_scd2` table with `customer_sk`, `customer_id`, `address`, `valid_from`, `valid_to`, `is_current`.
- [ ] Write an idempotent SQL script simulating an address update: close the active record (`valid_to = NOW(), is_current = FALSE`) and insert a new active record (`valid_from = NOW(), valid_to = NULL, is_current = TRUE`).
- [ ] Write a point-in-time lookup query fetching customer address as of 6 months ago.

## Completion Criteria
- [ ] Successfully design and populate an SCD Type 2 table.
- [ ] Query historical dimension attributes using point-in-time predicates (`WHERE :target_date BETWEEN valid_from AND COALESCE(valid_to, '9999-12-31')`).
- [ ] Compare architectural trade-offs between SCD Type 1 and SCD Type 2.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 (via Docker) | Relational database testing | Yes (Docker) | Yes | `docker run -d -p 5432:5432 postgres:16` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### SCD Type 2 Table Schema
```sql
CREATE TABLE dim_customers_scd2 (
    customer_sk BIGSERIAL PRIMARY KEY,
    customer_id INT NOT NULL,           -- Natural source key
    full_name VARCHAR(100) NOT NULL,
    state_code VARCHAR(2) NOT NULL,
    valid_from TIMESTAMP NOT NULL,
    valid_to TIMESTAMP,                 -- NULL if active
    is_current BOOLEAN NOT NULL DEFAULT TRUE
);
```

## Related Lessons
- Prerequisites: [[MOD-04 - Dimension Table Architecture]]
- Next Lesson: [[MOD-06 - Medallion Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
