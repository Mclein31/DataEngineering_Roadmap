---
id: AIR-02
title: Airflow 3 Architecture
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-02
---

# AIR-02 - Airflow 3 Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Apache Airflow 3.x architecture: Webserver, Scheduler, Metadata Database, Triggerer, and Executor workers.

## Concepts
- **Airflow 3.x Architectural Modernization**:
  - *Scheduler*: High-throughput heart of Airflow; parses DAG files, resolves dependencies, and queues task instances for execution.
  - *Metadata Database*: PostgreSQL or MySQL storing DAG states, task instance histories, connections, and variables.
  - *Executor & Workers*: Pluggable task runners (LocalExecutor, CeleryExecutor, KubernetesExecutor).
  - *Triggerer*: AsyncIO daemon handling deferred tasks (Sensors) with near-zero worker resource consumption.
  - *Webserver*: UI for inspecting DAG execution timelines, task logs, and triggering manual runs.

## Learning Resource
- **Title**: Apache Airflow 3.x Official Documentation
- **Provider / Author**: Apache Software Foundation
- **URL**: https://airflow.apache.org/docs/
- **Type**: Official Documentation
- **Topic**: Airflow 3 Architecture, Schedulers, Executors
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Deploy local Airflow via official Docker Compose configuration.
- [ ] Access the Airflow UI at `http://localhost:8080` (user/password: `airflow`).
- [ ] Inspect the metadata database schema in PostgreSQL to see `dag_run` and `task_instance` tables.

## Completion Criteria
- [ ] Deploy Airflow cleanly via Docker Compose.
- [ ] Explain the responsibilities of the Scheduler vs Executor vs Triggerer.
- [ ] Locate task execution logs in the Airflow Web UI.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Airflow (via Docker) | Workflow orchestration | Yes (Docker) | Yes | `curl -LfO 'https://airflow.apache.org/docs/apache-airflow/stable/docker-compose.yaml' && docker compose up -d` | https://airflow.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Airflow 3 Core Components
```text
[Webserver UI] <──> [Metadata Database (Postgres)] <──> [Scheduler]
                                │                              │
                        [Triggerer (Async)]             [Executor Queue]
                                                               │
                                                       [Worker Threads/Pods]
```

## Related Lessons
- Prerequisites: [[AIR-01 - Orchestration Principles]]
- Next Lesson: [[AIR-03 - TaskFlow API and Dynamic DAGs]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
