---
id: AIR-07
title: Resilient DAGs and Retries
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-07
---

# AIR-07 - Resilient DAGs and Retries

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build resilient, production-grade DAGs with automated retries, exponential backoff, SLA missed callbacks, and alerting hooks.

## Concepts
- **Task Retry Policies**:
  - `retries`: Number of attempts before marking task as `FAILED`.
  - `retry_delay`: Initial wait time between retries (`timedelta(minutes=5)`).
  - `retry_exponential_backoff`: Doubling delay between attempts to handle transient network blips.
  - `max_retry_delay`: Capping maximum backoff time.
- **Alerting & Callback Functions**:
  - `on_failure_callback`: Function executed upon final task failure (sends Slack/PagerDuty notification with run ID and log link).
  - `on_success_callback`, `on_retry_callback`.
- **SLA Miss Callbacks (`sla`)**: Triggering notifications if a critical daily pipeline has not finished by a specific business deadline.

## Learning Resource
- **Title**: Apache Airflow Documentation - Error Handling and Callbacks
- **Provider / Author**: Apache Software Foundation
- **URL**: https://airflow.apache.org/docs/apache-airflow/stable/administration-and-deployment/logging-monitoring/callbacks.html
- **Type**: Official Documentation
- **Topic**: Retries, Callbacks, SLA Monitoring
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure `default_args` on a DAG specifying 3 retries, exponential backoff, and 2-minute initial delay.
- [ ] Write an `on_failure_callback` function that formats and logs a simulated Slack webhook JSON payload.
- [ ] Test failure conditions by intentionally raising an exception in a task and verifying retry intervals in task logs.

## Completion Criteria
- [ ] Configure automated retries with exponential backoff on all network-dependent tasks.
- [ ] Implement an automated failure alerting callback function.
- [ ] Configure task timeouts (`execution_timeout=timedelta(hours=1)`) to terminate hung jobs.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Airflow 3.x | Resilience testing | Yes | Yes | `Docker Airflow` | https://airflow.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Production default_args Configuration
```python
from datetime import timedelta

default_args = {
    "owner": "data_engineering",
    "retries": 3,
    "retry_delay": timedelta(minutes=2),
    "retry_exponential_backoff": True,
    "max_retry_delay": timedelta(minutes=30),
    "execution_timeout": timedelta(hours=2),
    "on_failure_callback": notify_slack_failure
}
```

## Related Lessons
- Prerequisites: [[AIR-06 - Connections and Secrets]]
- Next Lesson: [[AIR-08 - Distributed Executors]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
