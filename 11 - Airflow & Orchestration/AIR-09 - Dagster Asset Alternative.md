---
id: AIR-09
title: Dagster Asset Alternative
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-09
---

# AIR-09 - Dagster Asset Alternative

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand Software-Defined Assets (SDAs) in Dagster as a modern asset-centric alternative to Airflow's workflow-centric DAGs.

## Concepts
- **Workflow-Centric vs Asset-Centric Orchestration**:
  - *Airflow (Legacy)*: Focuses on the *tasks* executed (e.g. "Run this Bash script, then run this Spark script").
  - *Dagster*: Focuses on the *data asset* produced (e.g. "Table `dim_users` exists, here is the Python code that defines it, and here are its upstream dependencies").
- **Software-Defined Assets (`@asset`)**: Declaring tables, files, and ML models as declarative assets with integrated schema checks and data lineage.
- **Why Airflow 3 Adopted Asset Concepts**: How Dagster's pioneering asset paradigm directly influenced Airflow 3's new Data-Aware Asset scheduling model.

## Learning Resource
- **Title**: Dagster Official Documentation - Software-Defined Assets
- **Provider / Author**: Elementl / Dagster
- **URL**: https://docs.dagster.io/concepts/assets/software-defined-assets
- **Type**: Official Documentation
- **Topic**: Dagster, Software-Defined Assets, Asset Lineage
- **Difficulty**: Intermediate
- **Category**: ⭐ RECOMMENDED

## Practice
- [ ] Install Dagster locally: `uv pip install dagster dagster-webserver`.
- [ ] Define two software-defined assets using `@asset` where `asset_b` depends on `asset_a`.
- [ ] Launch the Dagit/Dagster web UI: `dagster dev` and explore the asset dependency graph.

## Completion Criteria
- [ ] Explain the difference between task orchestration and asset orchestration.
- [ ] Build a 2-asset pipeline in Dagster.
- [ ] Articulate why both Airflow 3 and Dagster converged on asset-centric dependencies.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Dagster | Asset orchestration exploration | Yes | Yes | `uv pip install dagster dagster-webserver` | https://dagster.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Dagster Software-Defined Asset Example
```python
from dagster import asset

@asset
def raw_orders() -> list[dict]:
    return [{"id": 1, "amount": 100.0}]

@asset
def fct_orders(raw_orders: list[dict]) -> list[dict]:
    return [{**row, "tax": row["amount"] * 0.08} for row in raw_orders]
```

## Related Lessons
- Prerequisites: [[AIR-04 - Data-Aware Asset Scheduling]]
- Next Lesson: [[KFK-01 - Event-Driven Fundamentals]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
