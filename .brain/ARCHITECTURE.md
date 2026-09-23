---
type: project-brain
title: Data Engineering Roadmap — Architecture & Design
project: DataEngineering_Roadmap
last_updated: 2026-09-23
---

# 🏛️ Vault Architecture & Knowledge Design

## 1. Information Architecture
The vault is organized into a modular, progressive structure supporting both linear study (Phase 1 through Phase 5) and random-access reference (Dashboard, Resources, Certifications, Interview Prep).

```text
                           ┌───────────────────────────┐
                           │      00 - Dashboard       │
                           │   (Home, Logs, Matrix)    │
                           └─────────────┬─────────────┘
                                         │
                   ┌─────────────────────┴─────────────────────┐
                   ▼                                           ▼
       ┌───────────────────────┐                   ┌───────────────────────┐
       │     01 - Roadmap      │                   │ 18 - 21 Reference Hub │
       │  (Phases, 12 Months)  │                   │ (Projects, Certs, QA) │
       └───────────┬───────────┘                   └───────────────────────┘
                   │
                   ▼
       ┌────────────────────────────────────────────────────────┐
       │          Curriculum Modules (02 through 17)            │
       │   137 Granular Lessons with Metadata & DoD Criteria    │
       └────────────────────────────────────────────────────────┘
```

## 2. Note Structure & Frontmatter Schema
Each curriculum note conforms to a strict 9-section template with YAML frontmatter:
```yaml
---
id: LNX-01
title: Shell Navigation and Permissions
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-01
---
```
### Required Sections:
1. `## Status`: Checkbox tracker (`Not Started`, `In Progress`, `Completed`)
2. `## Objective`: Measurable technical capability
3. `## Concepts`: In-depth theoretical and low-level mechanics
4. `## Learning Resource`: Curated primary material with metadata and official URLs
5. `## Practice`: Terminal or coding exercises
6. `## Completion Criteria`: Definition of Done (DoD) verification checklist
7. `## Software / Tools`: macOS compatibility table (Apple Silicon/Intel, Free status, brew commands)
8. `## Notes`: Architecture diagrams, reference implementations, and production gotchas
9. `## Related Lessons`: Bidirectional links to prerequisites and subsequent lessons

## 3. Tooling & Platform Compatibility
- **OS**: macOS Sonoma & Sequoia (Native Apple Silicon ARM64 & Intel x86_64)
- **Local Emulation**: Docker Compose, LocalStack (AWS APIs), MinIO (S3 object storage)
- **Programming & Analysis**: Python 3.12+, uv package manager, Polars, DuckDB, PyArrow, Pytest
- **Orchestration & Streaming**: Apache Airflow 3.x, Apache Kafka 4.0 (KRaft mode)
- **Transformation & Lakehouse**: dbt-core, Apache Iceberg, Delta Lake UniForm, Apache Spark 4.0
