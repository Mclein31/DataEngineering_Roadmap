---
id: GOV-02
title: Column Masking and Row-Level Security
phase: Phase 4
module: Module 16: Data Governance & Security Engineering
aliases:
  - GOV-02
---

# GOV-02 - Column Masking and Row-Level Security

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Enforce dynamic column-level PII masking and Row-Level Security (RLS) policies without duplicating data tables.

## Concepts
- **Dynamic Column Masking**: Selectively obfuscating sensitive fields (SSN, credit card, email) at query time based on user role (e.g. `analyst` sees `***-**-1234`, while `compliance` sees raw value).
- **Row-Level Security (RLS)**: Filtering rows returned by queries transparently based on user attributes (e.g., regional manager in EMEA only sees rows where `region = 'EMEA'`).
- **Cryptographic Hashing & Salted Hashes**: Hashing customer identifiers (`SHA256(customer_id || salt)`) to allow analytical join aggregation without exposing raw identity.

## Learning Resource
- **Title**: PostgreSQL 16 Documentation - Row Security Policies
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/ddl-rowsecurity.html
- **Type**: Official Documentation
- **Topic**: Row-Level Security (RLS), Dynamic Masking, PII
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Enable RLS on a table in PostgreSQL: `ALTER TABLE orders ENABLE ROW LEVEL SECURITY;`.
- [ ] Create a policy restricting rows based on `CURRENT_USER`: `CREATE POLICY regional_isolation ON orders USING (region = CURRENT_USER);`.
- [ ] Write a view applying dynamic masking to email addresses using `REGEXP_REPLACE`.

## Completion Criteria
- [ ] Implement Row-Level Security (RLS) restricting query results per user.
- [ ] Apply dynamic column masking to sensitive financial or PII columns.
- [ ] Explain why data duplication is an anti-pattern for security enforcement.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | RLS testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### PostgreSQL Row-Level Security
```sql
ALTER TABLE sales_records ENABLE ROW LEVEL SECURITY;

CREATE POLICY regional_manager_policy ON sales_records
FOR SELECT
TO regional_managers
USING (region = current_setting('app.current_region'));
```

## Related Lessons
- Prerequisites: [[GOV-01 - Access Control Models RBAC ABAC]]
- Next Lesson: [[GOV-03 - Data Encryption at Rest and Transit]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
