---
id: KFK-08
title: Change Data Capture Debezium
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-08
---

# KFK-08 - Change Data Capture Debezium

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Stream database mutations (INSERT, UPDATE, DELETE) directly into Kafka in real time using Debezium Change Data Capture (CDC).

## Concepts
- **Change Data Capture (CDC) vs Batch Polling**: Why polling `WHERE updated_at > ...` misses deleted rows, causes read locks on OLTP, and creates polling latency.
- **Debezium Architecture**: Reading database transaction logs directly (PostgreSQL WAL via `pgoutput` logical decoding plugin, MySQL binlog).
- **CDC Event Envelope**:
  - `before`: Tuple state before mutation (null for insert).
  - `after`: Tuple state after mutation (null for delete).
  - `op`: Operation type (`c` = create, `u` = update, `d` = delete, `r` = read snapshot).
  - `source`: Database transaction metadata, LSN, timestamp.

## Learning Resource
- **Title**: Debezium Official Documentation - PostgreSQL Connector
- **Provider / Author**: Red Hat / Debezium Community
- **URL**: https://debezium.io/documentation/reference/stable/connectors/postgresql.html
- **Type**: Official Documentation
- **Topic**: Change Data Capture, Debezium, WAL Decoding
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure PostgreSQL with `wal_level = logical`.
- [ ] Deploy Kafka Connect with Debezium PostgreSQL connector container.
- [ ] Register a connector watching the `customers` table and verify that every `UPDATE` or `DELETE` produces an event into Kafka with `before` and `after` blocks.

## Completion Criteria
- [ ] Configure PostgreSQL logical replication for Debezium CDC.
- [ ] Parse Debezium CDC JSON envelopes to extract insert and delete mutations.
- [ ] Explain why CDC introduces near-zero read overhead on OLTP database instances.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Debezium Connect (Docker) | Change Data Capture | Yes | Yes | `debezium/connect` | https://debezium.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Debezium Event Envelope
```json
{
  "op": "u",
  "before": {"id": 1, "address": "123 Old St"},
  "after": {"id": 1, "address": "456 New Ave"},
  "source": {"lsn": 2498214, "ts_ms": 1727083200000}
}
```

## Related Lessons
- Prerequisites: [[DB-02 - Write-Ahead Logging and Durability]], [[KFK-03 - Broker Internals and Log Partitions]]
- Next Lesson: [[KFK-09 - Stream Processing Patterns]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
