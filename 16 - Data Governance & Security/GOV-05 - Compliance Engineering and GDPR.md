---
id: GOV-05
title: Compliance Engineering and GDPR
phase: Phase 4
module: Module 16: Data Governance & Security Engineering
aliases:
  - GOV-05
---

# GOV-05 - Compliance Engineering and GDPR

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Engineer data platforms for legal and regulatory compliance: GDPR 'Right to be Forgotten', CCPA, and automated data retention policies.

## Concepts
- **The Regulatory Mandate**: GDPR (General Data Protection Regulation), CCPA, and HIPAA.
- **The "Right to be Forgotten" (Article 17)**: Deleting all Personally Identifiable Information (PII) of a user upon request across all historical backups and lakehouse tables within 30 days.
- **The Immutability vs Deletion Conflict**: How to delete a single customer from immutable, append-only Parquet files on object storage:
  - *ACID Lakehouse MERGE / DELETE*: Rewriting only the affected Parquet data files using Apache Iceberg or Delta Lake.
  - *Crypto-Shredding*: Encrypting each customer's PII with a unique key; deleting the customer's key renders all historical data unreadable ciphertext.
- **Audit Trails**: Retaining immutable, non-repudiable access logs via AWS CloudTrail.

## Learning Resource
- **Title**: Designing Data-Intensive Applications - Security and Privacy
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: GDPR Compliance, Crypto-Shredding, Right to be Forgotten
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Execute an ACID `DELETE FROM customers WHERE customer_id = 9482` in an Apache Iceberg table.
- [ ] Verify that old snapshot files containing the deleted record are purged upon running Iceberg's expire snapshots procedure.
- [ ] Evaluate the operational complexity of crypto-shredding vs lakehouse physical deletion.

## Completion Criteria
- [ ] Implement a GDPR erasure workflow on an Apache Iceberg lakehouse table.
- [ ] Explain the cryptographic mechanism of crypto-shredding.
- [ ] Configure automated snapshot expiration to permanently remove deleted data from object storage.

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
### GDPR Erasure in Apache Iceberg
```sql
-- Step 1: Execute logical delete
DELETE FROM local.lakehouse.customers WHERE customer_id = 4821;

-- Step 2: Expire old snapshots containing the historical data file
CALL local.system.expire_snapshots(
    table => 'lakehouse.customers',
    older_than => TIMESTAMP '2026-09-23 00:00:00.000',
    retain_last => 1
);
-- Step 3: Remove orphaned data files
CALL local.system.remove_orphan_files(table => 'lakehouse.customers');
```

## Related Lessons
- Prerequisites: [[LAK-05 - Apache Iceberg Architecture]], [[GOV-02 - Column Masking and Row-Level Security]]
- Next Lesson: [[DES-01 - System Design Interview Framework]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
