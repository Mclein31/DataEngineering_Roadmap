---
title: Portfolio Presentation Playbook
aliases:
  - Portfolio Presentation Playbook
---

# 🎬 Portfolio Presentation & Defense Playbook

How to present your 5 portfolio repositories to engineering hiring managers, lead technical architectural walkthroughs, and defend design trade-offs.

---

## 📋 The 5-Minute Architectural Defense Script

When presenting a portfolio project (e.g., [[Project 5 - Converged Enterprise Lakehouse/README|Project 5]]):

### Minute 1: The Business Problem & Scale
- *"In this project, I addressed the challenge of unifying high-velocity streaming clickstream telemetry with daily batch financial transactions."*
- State functional and non-functional requirements: SLA, throughput (10,000 events/sec), latency bounds (<5 seconds).

### Minute 2: High-Level Architecture & Engine Selection
- Walk through your Mermaid architecture diagram.
- Defend your tech stack choices: *Why Kafka KRaft instead of RabbitMQ? Why Apache Iceberg instead of raw Parquet on S3?*

### Minute 3: Deep Technical Challenge Overcome
- Highlight a difficult engineering obstacle you solved:
  - Mitigating data skew in distributed joins.
  - Handling late-arriving streaming events outside the watermark.
  - Preserving column-level lineage across Spark and dbt into Marquez.

### Minute 4: Observability, Testing & Data Quality
- Showcase your automated test suite:
  - Demonstrate GitHub Actions CI executing `ruff`, `mypy --strict`, and `pytest`.
  - Show Soda Core data contract assertions catching dirty data in real time.

### Minute 5: Lessons Learned & Production Trade-Offs
- Explain what you would architect differently at 100x scale.
- Discuss cost trade-offs and operational maintenance.
