---
id: AIR-03
title: TaskFlow API and Dynamic DAGs
phase: Phase 3
module: Module 11: Workflow Orchestration with Airflow 3.x
aliases:
  - AIR-03
---

# AIR-03 - TaskFlow API and Dynamic DAGs

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build modern Airflow DAGs using the Python `@task` and `@dag` TaskFlow API decorators and dynamic task mapping.

## Concepts
- **TaskFlow API (`@task`, `@dag`)**: Decorator-driven Python syntax eliminating legacy operator boilerplate (`PythonOperator`, `BashOperator`).
- **Implicit XCom Handling**: Returning values from `@task` functions automatically handles serialization and deserialization via XComs.
- **Dynamic Task Mapping (`.expand()`)**: Dynamically generating parallel task instances at runtime based on an upstream list (e.g., mapping across 50 API endpoints).
- **Passing Complex Data**: Best practice: pass object storage URIs (S3/Parquet paths) through XComs rather than large in-memory dataframes.

## Learning Resource
- **Title**: Apache Airflow Documentation - TaskFlow API Tutorial
- **Provider / Author**: Apache Software Foundation
- **URL**: https://airflow.apache.org/docs/apache-airflow/stable/tutorial/taskflow.html
- **Type**: Official Documentation
- **Topic**: TaskFlow API, Dynamic Task Mapping, XComs
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write an extraction DAG using `@dag` and `@task` decorators in `dags/ecommerce_pipeline.py`.
- [ ] Implement dynamic task mapping to process 5 distinct product categories in parallel using `.expand()`.
- [ ] Pass Parquet output paths between extract, transform, and load tasks via returned XCom values.

## Completion Criteria
- [ ] Build a working 3-step DAG using the TaskFlow API.
- [ ] Implement dynamic task mapping using `.expand()`.
- [ ] Explain why large DataFrames must never be passed directly through standard metadata XComs.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Airflow | DAG development | Yes | Yes | `Docker Airflow` | https://airflow.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### TaskFlow API Example
```python
from airflow.decorators import dag, task
from datetime import datetime

@dag(schedule=None, start_date=datetime(2026, 1, 1), catchup=False)
def etl_pipeline():
    @task
    def extract() -> list[str]:
        return ["cat_electronics", "cat_clothing", "cat_home"]
    
    @task
    def process_category(category: str) -> str:
        return f"s3://bucket/curated/{category}.parquet"

    @task
    def load_marts(paths: list[str]):
        print(f"Loading {len(paths)} datasets into dimensional marts")

    categories = extract()
    curated_paths = process_category.expand(category=categories)
    load_marts(curated_paths)

pipeline = etl_pipeline()
```

## Related Lessons
- Prerequisites: [[AIR-02 - Airflow 3 Architecture]]
- Next Lesson: [[AIR-04 - Data-Aware Asset Scheduling]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
