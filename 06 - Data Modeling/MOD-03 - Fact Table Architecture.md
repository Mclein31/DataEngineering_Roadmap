---
id: MOD-03
title: Fact Table Architecture
phase: Phase 2
module: Module 06: Data Modeling & Schema Design
aliases:
  - MOD-03
---

# MOD-03 - Fact Table Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Classify, design, and optimize the three core Fact table patterns: Transactional, Periodic Snapshot, and Accumulating Snapshot.

## Concepts
- **Fact Table Fundamentals**: Numerical measurements and metrics resulting from a business event, foreign keys to dimensions, and additive behavior.
- **Core Fact Table Types**:
  - **Transaction Fact**: One row per discrete event (e.g., individual cashier scan). Most granular, highly additive, append-heavy.
  - **Periodic Snapshot Fact**: One row per defined time interval capturing cumulative state (e.g., daily bank account balances, monthly inventory snapshots). Semi-additive across time.
  - **Accumulating Snapshot Fact**: One row per entire lifecycle of an entity with multiple milestone date keys (e.g., order fulfillment: order date, ship date, delivery date). In-place update heavy.
- **Fact Additivity**: Fully Additive (sum across all dims), Semi-Additive (cannot sum across date dim, e.g. bank balance), Non-Additive (ratios, unit prices).
- **Factless Fact Tables**: Tracking occurrences without numerical metrics (e.g., student class attendance, hospital event logs).

## Learning Resource
- **Title**: The Data Warehouse Toolkit (Chapter 2: Fact Table Sizing and Patterns)
- **Provider / Author**: Ralph Kimball & Margy Ross (Wiley)
- **URL**: https://www.wiley.com/en-us/The+Data+Warehouse+Toolkit%3A+The+Definitive+Guide+to+Dimensional+Modeling%2C+3rd+Edition-p-9781118530801
- **Type**: Textbook
- **Topic**: Fact Tables, Additive Metrics, Snapshot Models
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Design a `fct_order_fulfillment` accumulating snapshot table with milestones for order placed, payment authorized, warehouse packed, carrier shipped, and customer delivered.
- [ ] Write SQL aggregations calculating end-of-month inventory levels from a periodic snapshot table.
- [ ] Construct a factless fact table tracking college course registration events.

## Completion Criteria
- [ ] Accurately distinguish between Transaction, Periodic Snapshot, and Accumulating Snapshot fact tables.
- [ ] Correctly identify non-additive metrics and prevent erroneous summation.
- [ ] Declare the exact grain for each fact table created.

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
### Fact Additivity Cheat Sheet
- **Additive**: Sales revenue, quantities sold, click counts (can `SUM` across all dimensions).
- **Semi-Additive**: Account balance, inventory levels (can `SUM` across stores, but must `AVG` or take end-of-period across time).
- **Non-Additive**: Unit prices, profit margins, conversion percentages (must compute from raw additive components).

## Related Lessons
- Prerequisites: [[MOD-02 - Kimball Dimensional Modeling]]
- Next Lesson: [[MOD-04 - Dimension Table Architecture]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
