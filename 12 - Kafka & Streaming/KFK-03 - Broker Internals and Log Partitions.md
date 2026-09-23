---
id: KFK-03
title: Broker Internals and Log Partitions
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-03
---

# KFK-03 - Broker Internals and Log Partitions

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Kafka broker storage internals: Topics, Partitions, Log Segments, Sparse Index files, and OS page cache zero-copy reads.

## Concepts
- **Topic Partitioning**: The unit of scalability and parallelism. A topic is split into multiple independent physical partition logs distributed across brokers.
- **Log Segments on Disk**: Partitions are divided into rolling segments (default 1GB or 7 days):
  - `.log`: Raw binary messages.
  - `.index`: Sparse index mapping logical offsets to physical byte positions.
  - `.timeindex`: Sparse index mapping timestamps to offsets.
- **Linux Zero-Copy (`sendfile`)**: Transferring data directly from OS Page Cache to Network Socket without copying bytes into JVM user space.
- **Retention Policies**: Deleting old segments based on retention time (`log.retention.hours`) or total size (`log.retention.bytes`).

## Learning Resource
- **Title**: Kafka: The Definitive Guide (2nd Edition) - Chapter 6: Kafka Internals
- **Provider / Author**: Gwen Shapira et al. (Confluent)
- **URL**: https://www.confluent.io/resources/kafka-the-definitive-guide-2nd-edition/
- **Type**: Free Official eBook
- **Topic**: Partitions, Log Segments, Zero-Copy I/O
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Inspect the physical files inside Kafka's log directory (`/tmp/kraft-combined-logs/orders-0/`).
- [ ] Use `kafka-run-class.sh kafka.tools.DumpLogSegments` to inspect raw message offsets and binary payloads inside `.log` files.
- [ ] Measure the impact of zero-copy reads on CPU utilization during high-throughput consumption.

## Completion Criteria
- [ ] Explain how sparse index files enable fast binary search for message offsets.
- [ ] Describe the Linux `sendfile` zero-copy network transfer mechanism.
- [ ] Calculate topic partition sizing based on producer throughput and consumer processing capacity.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Kafka (via Docker) | Log segment inspection | Yes | Yes | `Docker Kafka` | https://kafka.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Log Segment Files
```text
/tmp/kafka-logs/orders-0/
├── 00000000000000000000.index      (Offset-to-byte sparse index)
├── 00000000000000000000.timeindex  (Timestamp-to-offset sparse index)
└── 00000000000000000000.log        (Actual message payloads)
```

## Related Lessons
- Prerequisites: [[KFK-02 - Kafka 4 KRaft Consensus]]
- Next Lesson: [[KFK-04 - Producer Mechanics and Idempotence]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
