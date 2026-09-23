---
id: AIR-08
title: Distributed Executors
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-08
---

# AIR-08 - Distributed Executors

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Scale Airflow task execution across distributed worker clusters using CeleryExecutor and KubernetesExecutor.

## Concepts
- **Airflow Executor Architecture**:
  - `SequentialExecutor`: Default sqlite dev executor; runs one task at a time.
  - `LocalExecutor`: Runs tasks as multi-threaded/multi-process workers on the scheduler machine.
  - `CeleryExecutor`: Distributed queue architecture using Redis or RabbitMQ as broker, distributing tasks across a pool of persistent worker servers.
  - `KubernetesExecutor`: Ephemeral worker architecture; spins up an isolated Kubernetes Pod per task instance and tears it down upon completion.
- **Resource Isolation**: Why KubernetesExecutor eliminates dependency conflicts by allowing each task to specify a different Docker container image.

## Learning Resource
- **Title**: Apache Airflow Documentation - Executors Overview
- **Provider / Author**: Apache Software Foundation
- **URL**: https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/executor/index.html
- **Type**: Official Documentation
- **Topic**: Executors, Celery, KubernetesExecutor
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Review executor configurations in `airflow.cfg`.
- [ ] Compare resource overhead and task startup latency between CeleryExecutor (warm workers, fast start, shared env) and KubernetesExecutor (cold start, isolated pods).

## Completion Criteria
- [ ] Compare architectural trade-offs between CeleryExecutor and KubernetesExecutor.
- [ ] Explain how task instances transition from `QUEUED` to `RUNNING` through executor queues.
- [ ] Size worker concurrency (`worker_concurrency`) appropriately based on CPU/RAM bounds.

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
### Executor Trade-Off Matrix
| Feature | LocalExecutor | CeleryExecutor | KubernetesExecutor |
| :--- | :--- | :--- | :--- |
| **Cluster Scaling** | Single VM | Multi-Node Pool | Auto-scaling K8s Pods |
| **Startup Latency** | < 1 second | < 1 second | 5–30 seconds (Pod spinup) |
| **Dependency Isolation** | Shared | Shared worker | Total (Per-task Docker image) |

## Related Lessons
- Prerequisites: [[AIR-02 - Airflow 3 Architecture]]
- Next Lesson: [[AIR-09 - Dagster Asset Alternative]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
