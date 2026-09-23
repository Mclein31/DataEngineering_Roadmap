---
id: DES-02
title: Pipeline Idempotency and Backfills
phase: Phase 5
module: Module 17: Enterprise System Design & Architecture
aliases:
  - DES-02
---

# DES-02 - Pipeline Idempotency and Backfills

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect resilient, idempotent data pipelines capable of deterministic historical backfilling without data corruption.

## Concepts
- **The Idempotency Imperative**: Executing a pipeline $N$ times with identical input parameters must yield the exact same storage state ($f(f(x)) = f(x)$).
- **Core Idempotency Patterns**:
  - *Atomic Partition Overwrite*: Writing output to a temporary staging partition, then atomically replacing the target partition (`INSERT OVERWRITE` / dynamic partition replacement).
  - *ACID Upserts (`MERGE INTO`)*: Matching on unique business keys; updating existing rows and inserting new ones.
  - *Natural Key Deduplication*: Using deterministic hashes in downstream dimensional models.
- **Historical Backfill Architectures**: Parameterizing pipeline DAGs by logical execution dates (`execution_date`) rather than system runtime (`NOW()`).

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Chapter 10: Batch Processing)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: Idempotency, Backfills, Atomic Overwrites
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Refactor an extraction script that uses `datetime.now()` to accept an explicit `--logical-date YYYY-MM-DD` argument.
- [ ] Implement an atomic partition overwrite pattern in DuckDB / PySpark writing to an Iceberg table.
- [ ] Execute an automated 30-day historical backfill loop and verify zero duplicate rows in the final mart.

## Completion Criteria
- [ ] Build a pipeline that produces identical output across multiple executions.
- [ ] Use atomic partition overwrites instead of fragile delete-then-insert steps.
- [ ] Parameterize pipelines for historical deterministic backfilling.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Terraform & AWS CLI | IaC and cloud interaction | Yes (Native) | Yes | `brew install terraform awscli` | https://developer.hashicorp.com/terraform |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Atomic Partition Replacement Pattern
```sql
-- Atomic replacement guarantees readers never see an empty or half-written table
INSERT OVERWRITE TABLE marts.fct_daily_orders
PARTITION (order_date = '2026-09-23')
SELECT * FROM staging.stg_orders
WHERE order_date = '2026-09-23';
```

## Related Lessons
- Prerequisites: [[DES-01 - System Design Interview Framework]]
- Next Lesson: [[DES-03 - Architecture Patterns Batch vs Stream]]
- Phase Overview: [[Phase 5 - Systems & Career]]
