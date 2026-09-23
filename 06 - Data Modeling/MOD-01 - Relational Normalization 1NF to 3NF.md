---
id: MOD-01
title: Relational Normalization 1NF to 3NF
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-01
---

# MOD-01 - Relational Normalization 1NF to 3NF

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Design normalized relational schemas for operational systems, eliminating update, insert, and delete anomalies.

## Concepts
- **Relational Normal Forms**:
  - `1NF (First Normal Form)`: Atomic column values, unique rows (primary key), no repeating groups or comma-separated lists.
  - `2NF (Second Normal Form)`: In 1NF and all non-key attributes are fully functionally dependent on the entire primary key (eliminates partial key dependencies in composite keys).
  - `3NF (Third Normal Form)`: In 2NF and no transitive functional dependencies (non-key attribute depends on another non-key attribute).
- **Modification Anomalies**: Update anomalies (inconsistent edits), Insertion anomalies (unable to insert parent without child), Deletion anomalies (deleting child drops parent).
- **Trade-Offs**: Why 3NF is optimal for OLTP (fast writes, zero redundancy) but terrible for OLAP (requires dozens of joins).

## Learning Resource
- **Title**: The Data Warehouse Toolkit (Chapter 1: Elements of Dimensional Modeling)
- **Provider / Author**: Ralph Kimball & Margy Ross (Wiley)
- **URL**: https://www.wiley.com/en-us/The+Data+Warehouse+Toolkit%3A+The+Definitive+Guide+to+Dimensional+Modeling%2C+3rd+Edition-p-9781118530801
- **Type**: Textbook
- **Topic**: Relational Normalization, 3NF vs Dimensional
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Take a flat, denormalized 50-column spreadsheet containing orders, customers, and product details.
- [ ] Deconstruct it into 1NF, 2NF, and finally a fully compliant 3NF relational schema with primary and foreign keys.
- [ ] Identify and document an update anomaly present in the denormalized sheet.

## Completion Criteria
- [ ] Successfully decompose an unnormalized dataset into 3NF.
- [ ] Explain transitive dependency with a concrete business example.
- [ ] Articulate why analytical warehouses reject 3NF in favor of Star Schemas.

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
### Normalization Progression
```text
Unnormalized Data (Repeating groups, multi-valued cells)
    ↓
1NF (Atomic columns, Primary Key established)
    ↓
2NF (No partial key dependencies on composite keys)
    ↓
3NF (No transitive dependencies: non-key depends ONLY on the primary key)
```

## Related Lessons
- Prerequisites: [[SQL-03 - Relational Joins and Anti-Joins]]
- Next Lesson: [[MOD-02 - Kimball Dimensional Modeling]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
