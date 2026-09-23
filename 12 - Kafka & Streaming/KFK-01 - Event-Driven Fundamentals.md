---
id: KFK-01
title: Event-Driven Fundamentals
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-01
---

# KFK-01 - Event-Driven Fundamentals

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand event-driven architecture, distributed append-only commit logs, and the foundational mechanics of Apache Kafka.

## Concepts
- **Batch vs Stream Processing**: Periodic polling of state snapshots vs continuous reaction to real-time events.
- **The Distributed Append-Only Commit Log**: Kafka topics as ordered, immutable sequences of event records appended to disk.
- **Record Structure**: Key, Value, Timestamp, Headers, Offset.
- **Decoupling Producers and Consumers**: Publishers write without knowledge of consumers; multiple independent consumers read at their own pace without impacting broker throughput.

## Learning Resource
- **Title**: Kafka: The Definitive Guide (2nd Edition) - Chapter 1: Meet Kafka
- **Provider / Author**: Gwen Shapira et al. (Confluent)
- **URL**: https://www.confluent.io/resources/kafka-the-definitive-guide-2nd-edition/
- **Type**: Free Official eBook
- **Topic**: Kafka Fundamentals, Commit Log, Event Streaming
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare message queues (RabbitMQ - deletes message on consume) vs distributed event logs (Kafka - retains message on disk for multiple consumers).
- [ ] Calculate network throughput required for ingesting 10,000 events/second at 500 bytes per event.

## Completion Criteria
- [ ] Explain why Kafka stores events on disk as an append-only log.
- [ ] Differentiate between traditional queue semantics and pub/sub commit log semantics.
- [ ] Describe how log immutability enables event sourcing and stream replaying.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker & Docker Compose | Container coordination | Yes (Docker) | Yes | `brew install --cask docker` | https://www.docker.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Commit Log Structure
```text
Offset:    0      1      2      3      4      5  (Append-Only Head)
Log:    [Event][Event][Event][Event][Event][Event] --->
           ^                    ^
           │                    └── Consumer B (Offset 4)
           └─────────────────────── Consumer A (Offset 0)
```

## Related Lessons
- Prerequisites: [[AIR-01 - Orchestration Principles]]
- Next Lesson: [[KFK-02 - Kafka 4 KRaft Consensus]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
