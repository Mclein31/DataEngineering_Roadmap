---
id: MOD-04
title: Dimension Table Architecture
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-04
---

# MOD-04 - Dimension Table Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Design robust, descriptive dimension tables featuring hierarchies, degenerate dimensions, role-playing dimensions, and outriggers.

## Concepts
- **Dimension Table Fundamentals**: Descriptive context, textual attributes, filtering, grouping, and slice-and-dice constraints. Wide rows with many descriptive columns.
- **Degenerate Dimensions**: Dimension keys stored directly inside the fact table without a corresponding dimension table (e.g., invoice number, transaction ID, order number).
- **Role-Playing Dimensions**: A single physical dimension table joined multiple times in the same fact table under different roles/aliases (e.g., `dim_date` referenced as `order_date`, `ship_date`, `delivery_date`).
- **Junk Dimensions**: Grouping miscellaneous low-cardinality flags and indicators (payment method, promotional flag, order status) into a single lookup table to prevent fact table bloat.
- **Outrigger Dimensions**: A dimension referencing another dimension (e.g., `dim_store` -> `dim_county`); why outriggers should be avoided unless strictly necessary.

## Learning Resource
- **Title**: The Data Warehouse Toolkit (Chapter 2: Dimension Patterns)
- **Provider / Author**: Ralph Kimball & Margy Ross (Wiley)
- **URL**: https://www.wiley.com/en-us/The+Data+Warehouse+Toolkit%3A+The+Definitive+Guide+to+Dimensional+Modeling%2C+3rd+Edition-p-9781118530801
- **Type**: Textbook
- **Topic**: Dimension Tables, Junk Dimensions, Role-Playing
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Design a `dim_junk_order_flags` table collapsing 5 discrete boolean flags into a single surrogate key.
- [ ] Write an analytical SQL query joining `fct_orders` against `dim_date` three times using table aliases (`order_dt`, `ship_dt`, `due_dt`).
- [ ] Identify a degenerate dimension in an existing transactional receipt schema.

## Completion Criteria
- [ ] Implement role-playing dimensions in SQL using clean table aliasing.
- [ ] Collapse low-cardinality status flags into a Junk Dimension.
- [ ] Articulate when an attribute belongs as a Degenerate Dimension in a fact table.

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
### Role-Playing Dimension Query
```sql
SELECT 
    f.order_id,
    dt_order.calendar_date as order_date,
    dt_ship.calendar_date as ship_date,
    f.revenue
FROM fct_orders f
JOIN dim_date dt_order ON f.order_date_sk = dt_order.date_sk
JOIN dim_date dt_ship ON f.ship_date_sk = dt_ship.date_sk;
```

## Related Lessons
- Prerequisites: [[MOD-03 - Fact Table Architecture]]
- Next Lesson: [[MOD-05 - Slowly Changing Dimensions]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
