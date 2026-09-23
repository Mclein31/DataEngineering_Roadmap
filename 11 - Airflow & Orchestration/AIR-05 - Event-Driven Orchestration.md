---
id: AIR-05
title: Event-Driven Orchestration
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-05
---

# AIR-05 - Event-Driven Orchestration

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement event-driven DAG execution using Airflow Sensors, Deferrable Operators, and Webhook triggers.

## Concepts
- **Sensors vs Deferrable Operators**:
  - *Standard Sensors*: Occupy a worker execution slot while polling, exhausting cluster worker capacity.
  - *Deferrable Operators (`deferrable=True`)*: Release the execution worker thread and register an async trigger with the `Triggerer` daemon. Wakes up worker only when the condition is met!
- **S3 / External File Watching**: Polling for file arrival (`S3KeySensor`) with zero worker slot starvation.
- **REST API Webhook Triggers**: Triggering DAGs via external HTTP POST requests (`/api/v1/dags/{dag_id}/dagRuns`).

## Learning Resource
- **Title**: Apache Airflow Documentation - Deferrable Operators & Triggers
- **Provider / Author**: Apache Software Foundation
- **URL**: https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/deferring.html
- **Type**: Official Documentation
- **Topic**: Deferrable Operators, Sensors, Triggerer
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure a `FileSensor` or `S3KeySensor` with `deferrable=True`.
- [ ] Observe that while waiting for the file to arrive, the task uses zero Celery/worker slots in the Airflow UI.
- [ ] Trigger an ad-hoc DAG run externally using `curl -X POST http://localhost:8080/api/v1/dags/test_dag/dagRuns` with basic auth.

## Completion Criteria
- [ ] Explain how Deferrable Operators prevent worker starvation compared to standard polling sensors.
- [ ] Configure a sensor with exponential backoff and timeout thresholds.
- [ ] Trigger a DAG run securely via the Airflow REST API.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Airflow 3.x | Event triggers | Yes | Yes | `Docker Airflow` | https://airflow.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Deferrable Sensor Configuration
```python
from airflow.sensors.filesystem import FileSensor

wait_for_file = FileSensor(
    task_id="wait_for_incoming_csv",
    filepath="/opt/airflow/data/incoming.csv",
    poke_interval=60,
    timeout=3600,
    deferrable=True, # Releases worker slot to Triggerer
    mode="reschedule"
)
```

## Related Lessons
- Prerequisites: [[AIR-04 - Data-Aware Asset Scheduling]]
- Next Lesson: [[AIR-06 - Connections and Secrets]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
