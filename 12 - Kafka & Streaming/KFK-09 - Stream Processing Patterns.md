---
id: KFK-09
title: Stream Processing Patterns
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-09
---

# KFK-09 - Stream Processing Patterns

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect enterprise stream processing systems using stateful stream patterns: Dual Sinks, Dead Letter Queues, and Outbox Pattern.

## Concepts
- **The Dual-Sink Pattern (Fast Path & Cold Path)**:
  - *Fast Path*: Streaming into low-latency analytical stores (TimescaleDB, ClickHouse) for real-time dashboards and alerting.
  - *Cold Path*: Streaming into append-only partitioned object storage (MinIO/S3) for long-term historical audits and batch retraining.
- **The Transactional Outbox Pattern**: Solving dual-write race conditions by writing business data and outbox events within the same atomic database transaction, polled by CDC.
- **Dead Letter Queues (DLQ)**: Routing corrupted or unparseable messages to a separate topic without crashing consumer threads or halting stream progression.

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Chapter 11: Stream Processing)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: Stream Processing Patterns, Dual Sinks, DLQs
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Implement a Dead Letter Queue routing pattern in a Python streaming consumer: valid events sink to database; malformed events forward to `orders_dlq`.
- [ ] Architect the dual-sink pipeline required for [[Project 3 - Real-Time Streaming Ingestion/README|Project 3 (Real-Time Fleet Streaming)]].

## Completion Criteria
- [ ] Implement a Dead Letter Queue (DLQ) pattern handling poisoned messages gracefully.
- [ ] Explain how the Transactional Outbox pattern guarantees consistency between databases and Kafka.
- [ ] Architect a dual-sink pipeline balancing low latency (fast path) with cost-effective persistence (cold path).

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
### Dual-Sink Architecture
```text
Kafka Telemetry Topic ──> Stream Processor
                               ├──> [Fast Path: TimescaleDB / Grafana] (< 5s Latency)
                               └──> [Cold Path: MinIO / Iceberg Parquet] (Hourly Batches)
```

## Related Lessons
- Prerequisites: [[KFK-06 - Delivery Guarantees]]
- Next Lesson: [[CLD-01 - AWS IAM Security]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
