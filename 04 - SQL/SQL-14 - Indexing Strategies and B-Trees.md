---
id: SQL-14
title: Indexing Strategies and B-Trees
phase: Phase 1
module: Module 04: Advanced SQL & Query Optimization
aliases:
  - SQL-14
---

# SQL-14 - Indexing Strategies and B-Trees

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Design composite, partial, and covered B-Tree indexes that maximize query velocity while minimizing write amplification.

## Concepts
- **B-Tree Index Architecture**: Balanced multi-way tree of 8KB index pages, root node, branch nodes, and doubly-linked leaf nodes storing sorted keys and TIDs.
- **The Leftmost Prefix Rule**: A composite index `(col_a, col_b)` can service queries on `col_a` alone or `(col_a, col_b)`, but CANNOT service queries filtering only on `col_b`.
- **Column Ordering Strategy**: Equality columns first, Range/Inequality columns second (`WHERE status = 'ACTIVE' AND created_at >= '2026-01-01'`).
- **Partial Indexes**: Filtering index construction (`CREATE INDEX ... WHERE is_active = true`), drastically reducing index disk footprint.
- **Covering Indexes (`INCLUDE`)**: Adding non-key payload columns to index leaf pages to enable Index Only Scans without participating in tree ordering.

## Learning Resource
- **Title**: Use The Index, Luke! - Anatomy of an Index
- **Provider / Author**: Markus Winand
- **URL**: https://use-the-index-luke.com/
- **Type**: Free Web Book
- **Topic**: B-Tree Architecture, Composite Indexing, Partial Indexes
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a composite index on a multi-filter query: `CREATE INDEX idx_orders_cust_date ON orders (customer_id, order_date DESC)`.
- [ ] Create a partial index for active subscription records: `CREATE INDEX idx_active_subs ON subscriptions (user_id) WHERE status = 'ACTIVE'`.
- [ ] Measure disk footprint differences between full index and partial index using `pg_relation_size()`.

## Completion Criteria
- [ ] Explain the Leftmost Prefix Rule in composite B-Tree indexes.
- [ ] Design an index that reduces execution time by > 80% on a multi-filter query.
- [ ] Articulate when to use the `INCLUDE` clause for covering indexes.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Indexing testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community / pgAdmin | GUI database client | Yes | Yes | Free universal SQL client |

## Notes
### Covered Index Example
```sql
-- Enables Index Only Scan for query retrieving total_amount for a specific customer
CREATE INDEX idx_orders_cust_covering 
ON orders (customer_id) 
INCLUDE (total_amount, order_date);
```

## Related Lessons
- Prerequisites: [[SQL-12 - Relational Access Methods]]
- Next Lesson: [[DB-01 - Row vs Columnar Storage]]
- Phase Overview: [[Phase 1 - Foundations]]
