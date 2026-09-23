---
id: DB-03
title: MVCC and Isolation Levels
phase: Phase 1
module: Module 05: Database Internals & Storage Engines
aliases:
  - DB-03
---

# DB-03 - MVCC and Isolation Levels

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Multi-Version Concurrency Control (MVCC), transaction snapshot isolation, and concurrency anomalies.

## Concepts
- **MVCC Architecture**: Readers never block writers, and writers never block readers. Rows are not updated in place; updates create new tuple versions.
- **Tuple Header Metadata**: `xmin` (creating transaction ID), `xmax` (deleting/updating transaction ID), `t_ctid` (tuple pointer).
- **ANSI SQL Isolation Levels**:
  - `Read Committed`: Sees data committed before each individual statement begins.
  - `Repeatable Read`: Snapshot isolation; sees data committed before the transaction began. Prevents non-repeatable reads.
  - `Serializable`: Strict serial order using Snapshot Isolation (SSI) to prevent write skew.
- **Concurrency Anomalies**: Dirty reads, non-repeatable reads, phantom reads, write skew.

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Chapter 7: Transactions)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: MVCC, ACID, Transaction Isolation Levels
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Open two concurrent `psql` terminal sessions.
- [ ] Set `TRANSACTION ISOLATION LEVEL REPEATABLE READ` in Session 1, mutate and commit data in Session 2, and observe that Session 1 continues reading the immutable snapshot.
- [ ] Inspect row `xmin` and `xmax` system hidden columns: `SELECT xmin, xmax, * FROM orders;`.

## Completion Criteria
- [ ] Explain how PostgreSQL implements updates via dead tuple creation.
- [ ] Reproduce write skew under Repeatable Read and resolve it using Serializable isolation.
- [ ] Inspect transaction IDs using `txid_current()`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Concurrency testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### MVCC Tuple Header
```sql
SELECT ctid, xmin, xmax, * FROM customers;
-- ctid: Physical page and item pointer (e.g., (0, 1))
-- xmin: Transaction that inserted this row
-- xmax: Transaction that deleted or updated this row (0 if live)
```

## Related Lessons
- Prerequisites: [[DB-02 - Write-Ahead Logging and Durability]]
- Next Lesson: [[DB-04 - PostgreSQL Vacuum and Bloat]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
