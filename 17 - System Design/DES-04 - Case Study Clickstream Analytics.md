---
id: DES-04
title: Case Study Clickstream Analytics
phase: Phase 5
module: Module 17: Enterprise System Design & Architecture
aliases:
  - DES-04
---

# DES-04 - Case Study Clickstream Analytics

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect a real-time clickstream ingestion engine handling 100,000 events/second with sub-minute analytical query latency.

## Concepts
- **System Requirements**: Ingesting mobile and web pageviews, clicks, and session events at 100,000 events/second. Sub-minute latency for dashboard reporting, 5-year retention.
- **Capacity Calculations**:
  - Event size: ~500 bytes.
  - Throughput: $100,000 	imes 500 = 50	ext{ MB/sec} = 4.32	ext{ TB/day} pprox 1.57	ext{ PB/year}$.
  - Kafka Partitions: Assuming 5MB/s per partition $	o$ 10 partitions minimum (recommend 32 for scaling).
- **Architecture**:
  - Ingestion: API Gateway -> Kafka 4.0 KRaft -> Schema Registry.
  - Processing: Spark Structured Streaming / Flink sessionizing clickstreams with 30-min inactivity timeout.
  - Storage: Apache Iceberg on S3 partitioned by `day(event_time)` and bucketed by `user_id`.
  - Serving: Trino / StarRocks for sub-second analytical dashboard queries.

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Case Studies)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: Clickstream Architecture, High-Throughput System Design
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Execute a mock 45-minute system design defense for this clickstream architecture on a whiteboard.
- [ ] Address failure conditions: what happens when Kafka consumer lag surges during Black Friday traffic spikes?

## Completion Criteria
- [ ] Defend capacity calculations (MB/s and TB/year) for 100k events/sec.
- [ ] Design sessionization logic handling late-arriving events outside watermarks.
- [ ] Mitigate consumer lag surges using auto-scaling worker groups.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Terraform & AWS CLI | IaC and cloud interaction | Yes (Native) | Yes | `brew install terraform awscli` | https://developer.hashicorp.com/terraform |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Clickstream System Blueprint
```text
Clients ──> API Gateway ──> Kafka Topic (32 Partitions)
                                │
                        [Spark Streaming] (Watermarking: 15m)
                                ├──> [Fast Path: Redis / ClickHouse] (Live User Counts)
                                └──> [Cold Path: Iceberg / S3] (Long-Term Behavioral Lakehouse)
```

## Related Lessons
- Prerequisites: [[DES-03 - Architecture Patterns Batch vs Stream]]
- Next Lesson: [[DES-05 - Case Study Financial Ledger]]
- Phase Overview: [[Phase 5 - Systems & Career]]
