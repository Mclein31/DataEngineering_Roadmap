---
id: DES-06
title: Case Study IoT Telemetry Engine
phase: Phase 5
module: Module 17: Enterprise System Design & Architecture
aliases:
  - DES-06
---

# DES-06 - Case Study IoT Telemetry Engine

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect a massive IoT telemetry ingestion engine handling 1,000,000 connected devices with anomaly alerting and cold-path archival.

## Concepts
- **System Requirements**: 1,000,000 connected devices emitting telemetry every 10 seconds (100,000 events/sec sustained). Real-time anomaly detection (< 5s alert latency). Low-cost cold archival.
- **Handling Unreliable Connectivity**: Device clocks out of sync, network dropouts causing bursts of days-old late-arriving events.
- **Architecture**:
  - Ingestion: MQTT Brokers -> Kafka 4.0 KRaft cluster (Geo-replicated).
  - Stream Processing: Spark Structured Streaming / Flink calculating moving averages and anomaly thresholds.
  - Storage: TimescaleDB / ClickHouse for hot 7-day query map + Apache Iceberg on MinIO/S3 for cold 5-year archive.
  - Observability: Real-time Grafana fleet telemetry dashboards.

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Case Studies: IoT & Sensor Data)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: IoT Telemetry Architecture, High Scale Streaming, Timescale
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Defend this IoT architecture during a mock technical interview.
- [ ] Explain how you would prevent late-arriving telemetry bursts from overwhelming the stream state store.

## Completion Criteria
- [ ] Lead an architectural walkthrough of a 1M-device IoT streaming engine.
- [ ] Address clock drift and late-arriving sensor packets using watermarking.
- [ ] Detail the storage and cost trade-offs of hot vs cold path partitioning.

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
### IoT Telemetry Blueprint
```text
1M IoT Devices ──> MQTT Gateways ──> Kafka 4.0 Cluster (KRaft)
                                          │
                                  [Stream Processor]
                                  ├──> [Hot Path: TimescaleDB / Grafana] (Sub-5s Alerting)
                                  └──> [Cold Path: MinIO / Iceberg Parquet] (Partitioned Archive)
```

## Related Lessons
- Prerequisites: [[DES-05 - Case Study Financial Ledger]]
- Next Lesson: [[Project Index]]
- Phase Overview: [[Phase 5 - Systems & Career]]
