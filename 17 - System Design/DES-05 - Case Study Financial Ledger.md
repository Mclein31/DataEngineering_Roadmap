---
id: DES-05
title: Case Study Financial Ledger
phase: Phase 5
module: Module 17: Enterprise System Design & Architecture
aliases:
  - DES-05
---

# DES-05 - Case Study Financial Ledger

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect a double-entry financial ledger lakehouse guaranteeing strict ACID compliance, audit trails, and zero monetary discrepancy.

## Concepts
- **System Requirements**: Processing banking transactions with mathematical precision (no floating-point rounding errors). Double-entry bookkeeping (every transaction has debit and credit summing to zero). Immutable audit trail.
- **Zero-Discrepancy Data Engineering**:
  - Using exact numerical types (`DECIMAL(18, 4)`) exclusively.
  - Enforcing immutable append-only transaction logs.
  - Checksums and balance reconciliations executed at every pipeline stage.
- **Architecture**:
  - Ingestion: Transactional CDC (Debezium) from core banking database into Kafka.
  - Lakehouse Storage: Apache Iceberg on S3 with snapshot retention for immutable time-travel audits.
  - Automated Reconciliation: Daily dbt singular tests verifying account debits equal credits.

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Financial Systems Modeling)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Financial Ledgers, Double-Entry, ACID Audits
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Model a double-entry ledger schema in SQL with accounts, journal entries, and postings.
- [ ] Write an automated reconciliation query asserting $\sum(	ext{debits}) - \sum(	ext{credits}) = 0$.
- [ ] Execute an Iceberg time-travel query to audit account balances as of a specific fiscal quarter close.

## Completion Criteria
- [ ] Design an immutable double-entry ledger data model.
- [ ] Implement automated mathematical reconciliation tests in dbt or SQL.
- [ ] Demonstrate time-travel audit verification using Apache Iceberg.

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
### Double-Entry Balance Assertion
```sql
SELECT 
    journal_entry_id,
    SUM(CASE WHEN entry_type = 'DEBIT' THEN amount ELSE -amount END) as balance_delta
FROM journal_postings
GROUP BY journal_entry_id
HAVING SUM(CASE WHEN entry_type = 'DEBIT' THEN amount ELSE -amount END) != 0.00;
-- FAILS if any journal entry does not balance to exactly zero!
```

## Related Lessons
- Prerequisites: [[DES-04 - Case Study Clickstream Analytics]]
- Next Lesson: [[DES-06 - Case Study IoT Telemetry Engine]]
- Phase Overview: [[Phase 5 - Systems & Career]]
