---
id: DAT-05
title: OpenLineage and Marquez
phase: Phase 4
module: Module 15: Data Reliability Engineering & Observability
aliases:
  - DAT-05
---

# DAT-05 - OpenLineage and Marquez

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Capture automated, column-level runtime lineage across Spark and dbt using OpenLineage and visualize dependencies in Marquez.

## Concepts
- **The OpenLineage Standard**: Vendor-neutral open standard for metadata and lineage collection; emits events (`START`, `RUNNING`, `COMPLETE`, `FAIL`) with input/output dataset facets.
- **Marquez**: Open-source reference implementation of OpenLineage. Collects, stores, and visualizes job dependencies and dataset lineage graphs.
- **Automated Column-Level Lineage**: Tracking how individual columns are transformed from raw sources through Spark joins and dbt models to final dashboards without manual documentation.
- **Root-Cause Triage**: Tracing a broken BI dashboard metric upstream through Marquez to identify the exact failed Spark job or dirty source partition.

## Learning Resource
- **Title**: OpenLineage Official Documentation & Marquez Quickstart
- **Provider / Author**: OpenLineage Community
- **URL**: https://openlineage.io/docs/
- **Type**: Official Documentation
- **Topic**: OpenLineage, Marquez, Column-Level Lineage
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Deploy Marquez via Docker Compose: `docker run -d -p 3000:3000 -p 5000:5000 marquezproject/marquez`.
- [ ] Configure `dbt-core` or PySpark to emit OpenLineage events to `http://localhost:5000`.
- [ ] Execute a pipeline and inspect the interactive column-level lineage graph in the Marquez UI (`http://localhost:3000`).

## Completion Criteria
- [ ] Deploy Marquez locally via Docker.
- [ ] Emit OpenLineage events from a PySpark or dbt execution run.
- [ ] Trace an end-to-end lineage path from raw ingestion to final mart in the Marquez UI.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Marquez (Docker) | Lineage metadata collection & UI | Yes (Docker) | Yes | `docker run -p 3000:3000 -p 5000:5000 marquezproject/marquez` | https://marquezproject.ai/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Configuring dbt OpenLineage
Install adapter:
```bash
uv pip install openlineage-dbt
# Run dbt through OpenLineage wrapper
OPENLINEAGE_URL=http://localhost:5000 dbt-ol run
```

## Related Lessons
- Prerequisites: [[DBT-10 - dbt Documentation and Lineage]]
- Next Lesson: [[DAT-06 - Anomaly Detection and Alerting]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
