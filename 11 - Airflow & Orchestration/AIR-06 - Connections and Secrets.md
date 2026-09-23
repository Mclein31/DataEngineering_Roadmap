---
id: AIR-06
title: Connections and Secrets
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-06
---

# AIR-06 - Connections and Secrets

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Securely manage database credentials, API tokens, and cloud access keys using Airflow Connections, Secrets Backends, and environment variables.

## Concepts
- **Airflow Connections (`Hook` integration)**: Decoupling code from connection details (`conn_id="postgres_default"`).
- **Secrets Backend Integration**: Fetching secrets dynamically at runtime from external enterprise vaults (AWS Secrets Manager, HashiCorp Vault) rather than storing plain text in metadata DB.
- **Environment Variable Overrides**: Defining connections via environment variables: `AIRFLOW_CONN_POSTGRES_DEFAULT='postgresql://user:pass@host:5432/db'`.
- **Airflow Variables vs Connections**: Best practices: Variables for non-sensitive configurations; Connections/Secrets for credentials.

## Learning Resource
- **Title**: Apache Airflow Documentation - Managing Connections & Secrets
- **Provider / Author**: Apache Software Foundation
- **URL**: https://airflow.apache.org/docs/apache-airflow/stable/security/secrets/index.html
- **Type**: Official Documentation
- **Topic**: Connections, Secrets Backends, Security
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure a PostgreSQL connection in Airflow using environment variables in `docker-compose.yml`.
- [ ] Use `PostgresHook(postgres_conn_id='my_postgres')` in a Python task to query records without hardcoding credentials in the DAG file.
- [ ] Verify that sensitive passwords are masked with asterisks `***` in Airflow logs and UI.

## Completion Criteria
- [ ] Never hardcode credentials, passwords, or tokens in DAG Python files.
- [ ] Retrieve database connections cleanly via `BaseHook.get_connection()`.
- [ ] Verify automated masking of sensitive connection variables in execution logs.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Airflow 3.x | Secrets configuration | Yes | Yes | `Docker Airflow` | https://airflow.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Secure Hook Pattern
```python
from airflow.decorators import task
from airflow.providers.postgres.hooks.postgres import PostgresHook

@task
def extract_from_postgres():
    hook = PostgresHook(postgres_conn_id="retail_postgres")
    conn = hook.get_conn()
    with conn.cursor() as cur:
        cur.execute("SELECT order_id, amount FROM orders LIMIT 100;")
        return cur.fetchall()
```

## Related Lessons
- Prerequisites: [[AIR-03 - TaskFlow API and Dynamic DAGs]]
- Next Lesson: [[AIR-07 - Resilient DAGs and Retries]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
