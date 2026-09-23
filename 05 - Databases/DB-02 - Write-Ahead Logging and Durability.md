---
id: DB-02
title: Write-Ahead Logging and Durability
phase: Phase 2
module: Module 05: Database Internals & Storage Engines
aliases:
  - DB-02
---

# DB-02 - Write-Ahead Logging and Durability

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master Write-Ahead Logging (WAL), crash recovery mechanics, dirty page flushing, and the ARIES recovery algorithm.

## Concepts
- **The Write-Ahead Log (WAL) Principle**: Guaranteeing durability without synchronous random disk writes. Changes are appended sequentially to the WAL before dirty buffer pool pages are written to data files.
- **Log Sequence Numbers (LSN)**: Monotonically increasing byte offsets tracking transaction positions across the WAL and data pages.
- **Checkpoints**: Periodic flushing of dirty shared buffer pages to disk to bound crash recovery replay duration.
- **Group Commit**: Amortizing `fsync` disk latency by grouping concurrent transaction log writes into a single sequential flush.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - Write-Ahead Logging (WAL)
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/wal.html
- **Type**: Official Documentation
- **Topic**: WAL, Durability, Recovery, Checkpoints
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Inspect active PostgreSQL WAL settings (`wal_level`, `checkpoint_timeout`, `max_wal_size`).
- [ ] Measure disk write throughput difference between `synchronous_commit = on` and `synchronous_commit = off`.
- [ ] Force a checkpoint using `CHECKPOINT;` and observe buffer cache dirty page writes via `pg_stat_bgwriter`.

## Completion Criteria
- [ ] Explain how WAL guarantees Atomicity and Durability during sudden power loss.
- [ ] Describe the purpose of LSN markers on physical 8KB data pages.
- [ ] Articulate the trade-offs of tuning `checkpoint_completion_target` in high-throughput pipelines.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | WAL inspection | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### WAL Replay Architecture
```text
Application INSERT
       ↓
Append to WAL (Sequential I/O, fast) ──> Disk (WAL segment)
       ↓
Update Shared Buffer Page (in RAM)
       ↓
[Checkpoint] ──> Flushes Dirty Pages to Table Files (Random I/O)
```

## Related Lessons
- Prerequisites: [[DB-01 - Row vs Columnar Storage]]
- Next Lesson: [[DB-03 - MVCC and Isolation Levels]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
