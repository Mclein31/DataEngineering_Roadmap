---
id: DB-04
title: PostgreSQL Vacuum and Bloat
phase: Phase 2
module: Module 05: Database Internals & Storage Engines
aliases:
  - DB-04
---

# DB-04 - PostgreSQL Vacuum and Bloat

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Diagnose table and index bloat, understand the vacuum process, visibility maps, and freeze transaction ID wraparound.

## Concepts
- **Table & Index Bloat**: Dead tuples left behind by `UPDATE` and `DELETE` operations consuming disk space and degrading sequential scan performance.
- **Standard `VACUUM`**: Reclaims space within 8KB pages for future inserts and updates the Visibility Map; does NOT return disk space to OS.
- **`VACUUM FULL`**: Rewrites the entire table into a new file, reclaiming OS disk space, but requires an exclusive `ACCESS EXCLUSIVE` table lock.
- **Transaction ID Wraparound**: 32-bit transaction IDs wrap around every ~2 billion transactions; why `autovacuum_freeze_max_age` is critical.
- **Visibility Map**: Tracking pages containing zero dead tuples to accelerate `VACUUM` and enable `Index Only Scans`.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - Routine Vacuuming
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/routine-vacuuming.html
- **Type**: Official Documentation
- **Topic**: Vacuuming, Bloat, Transaction Wraparound
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Execute 100,000 updates on a 10,000 row table to intentionally induce massive dead tuple bloat.
- [ ] Query `pg_stat_user_tables` to inspect `n_dead_tup` vs `n_live_tup`.
- [ ] Run `VACUUM (VERBOSE, ANALYZE)` and observe dead tuple reclamation and Visibility Map updates.

## Completion Criteria
- [ ] Measure table bloat using `pg_stat_user_tables`.
- [ ] Explain why standard `VACUUM` does not shrink file sizes on disk.
- [ ] Explain the catastrophe of transaction ID wraparound and how autovacuum freeze mitigates it.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | Vacuum testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Dead Tuple Monitoring Query
```sql
SELECT 
    relname, 
    n_live_tup, 
    n_dead_tup, 
    ROUND(n_dead_tup * 100.0 / NULLIF(n_live_tup + n_dead_tup, 0), 2) as dead_tuple_ratio,
    last_vacuum, 
    last_autovacuum
FROM pg_stat_user_tables;
```

## Related Lessons
- Prerequisites: [[DB-03 - MVCC and Isolation Levels]]
- Next Lesson: [[DB-05 - Specialized PostgreSQL Indexes]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
