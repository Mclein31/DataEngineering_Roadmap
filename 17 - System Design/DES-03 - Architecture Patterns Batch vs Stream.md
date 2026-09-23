---
id: DES-03
title: Architecture Patterns Batch vs Stream
phase: Phase 5
module: Module 17: Enterprise System Design & Architecture
aliases:
  - DES-03
---

# DES-03 - Architecture Patterns Batch vs Stream

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Compare enterprise architectural paradigms: Lambda Architecture, Kappa Architecture, and Modern Lakehouse Convergence.

## Concepts
- **Lambda Architecture (Legacy Dual-Track)**:
  - *Speed Layer*: Low-latency stream processor (Storm/Flink) for real-time views.
  - *Batch Layer*: High-throughput batch engine (Hadoop/Spark) for immutable truth.
  - *Serving Layer*: Merges results from speed and batch views.
  - *Fatal Flaw*: Maintaining two completely separate codebases for the exact same business logic!
- **Kappa Architecture**: Single stream processing pipeline for both real-time and historical replay; historical data is simply re-read from the Kafka log.
- **Modern Lakehouse Convergence**: Unifying batch and streaming onto a single storage layer (Apache Iceberg) where streaming jobs continuously append micro-batches and batch jobs execute periodic transformations.

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Chapter 12: The Future of Data Systems)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: Lambda Architecture, Kappa Architecture, Convergence
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare Lambda vs Kappa vs Lakehouse Convergence across: operational complexity, latency, and code maintenance.
- [ ] Design an architectural migration plan moving an enterprise from legacy Lambda to Lakehouse Convergence.

## Completion Criteria
- [ ] Explain why the Lambda architecture was widely abandoned in modern data engineering.
- [ ] Describe how Lakehouse table formats (Iceberg) enable batch and stream convergence.
- [ ] Select appropriate architectural paradigms based on latency requirements.

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
### Architecture Comparison
| Pattern | Codebases | Storage Layers | Latency | Complexity |
| :--- | :--- | :--- | :--- | :--- |
| **Lambda** | 2 (Batch + Stream) | 2 (HDFS + Real-time DB) | Low | Very High |
| **Kappa** | 1 (Stream only) | 1 (Kafka log) | Low | Medium |
| **Lakehouse Convergence** | 1 (SQL / PySpark) | 1 (Apache Iceberg on S3) | Near-Real-Time (<1m) | Low |

## Related Lessons
- Prerequisites: [[DES-02 - Pipeline Idempotency and Backfills]]
- Next Lesson: [[DES-04 - Case Study Clickstream Analytics]]
- Phase Overview: [[Phase 5 - Systems & Career]]
