---
id: MOD-02
title: Kimball Dimensional Modeling
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-02
---

# MOD-02 - Kimball Dimensional Modeling

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect Kimball dimensional models (Star Schemas) that optimize analytical query velocity and business comprehensibility.

## Concepts
- **The 4-Step Dimensional Design Process**:
  1. Select the business process (e.g., Retail Sales).
  2. Declare the grain (e.g., one row per line item on a retail receipt).
  3. Identify the dimensions (e.g., Date, Customer, Store, Product, Promotion).
  4. Identify the facts (e.g., Quantity Sold, Extended Amount, Tax, Discount).
- **The Star Schema**: Central Fact table surrounded by denormalized Dimension tables with single-hop foreign key relationships.
- **Surrogate Keys vs Natural Keys**: Why integer/bigint surrogate keys (`customer_sk`) generated in the warehouse are mandatory over source natural business keys (`customer_id`).
- **Conformed Dimensions**: Shared dimensions (e.g., `dim_date`, `dim_customer`) across multiple enterprise business processes.

## Learning Resource
- **Title**: The Data Warehouse Toolkit (3rd Edition)
- **Provider / Author**: Ralph Kimball & Margy Ross (Wiley)
- **URL**: https://www.wiley.com/en-us/The+Data+Warehouse+Toolkit%3A+The+Definitive+Guide+to+Dimensional+Modeling%2C+3rd+Edition-p-9781118530801
- **Type**: Textbook
- **Topic**: Kimball Star Schema, Dimensional Modeling
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Execute the 4-step Kimball process for an e-commerce subscription platform.
- [ ] Draft an Entity-Relationship (ER) Star Schema diagram showing primary/foreign key connections.
- [ ] Explain why `dim_date` should be modeled as an explicit dimension table rather than relying purely on SQL timestamp parsing.

## Completion Criteria
- [ ] Recite and apply the 4-step Kimball design process to any business domain.
- [ ] Explain the critical difference between surrogate keys and natural source keys.
- [ ] Define what constitutes a Conformed Dimension in an enterprise data bus architecture.

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
### Star Schema Architecture
```text
       [dim_customer]         [dim_product]
             │                      │
             └──> [fct_sales] <─────┘
                     │    │
       [dim_date] <──┘    └──> [dim_store]
```

## Related Lessons
- Prerequisites: [[MOD-01 - Relational Normalization 1NF to 3NF]]
- Next Lesson: [[MOD-03 - Fact Table Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
