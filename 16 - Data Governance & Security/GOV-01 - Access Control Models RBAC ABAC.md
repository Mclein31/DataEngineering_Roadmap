---
id: GOV-01
title: Access Control Models RBAC ABAC
phase: Phase 4
module: Module 16: Data Governance & Security Engineering
aliases:
  - GOV-01
---

# GOV-01 - Access Control Models RBAC ABAC

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Architect enterprise access governance models using Role-Based Access Control (RBAC) and Attribute-Based Access Control (ABAC).

## Concepts
- **Role-Based Access Control (RBAC)**: Granting permissions based on organizational job function (e.g. `data_engineer`, `financial_analyst`, `marketing_viewer`).
- **Attribute-Based Access Control (ABAC)**: Dynamic policy evaluation based on attributes of the user (department, security clearance), resource (data classification, environment), and environment (time, IP address).
- **Least-Privilege Object Grants in SQL**: `GRANT SELECT ON table TO ROLE analyst;` vs granular column grants.
- **Centralized Lakehouse Governance**: Why modern enterprises shift access control out of individual databases into centralized catalogs (Unity Catalog, Apache Polaris).

## Learning Resource
- **Title**: PostgreSQL Documentation - Database Roles & Privileges
- **Provider / Author**: PostgreSQL Global Development Group
- **URL**: https://www.postgresql.org/docs/current/user-manag.html
- **Type**: Official Documentation
- **Topic**: RBAC, ABAC, Access Control, Security
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create 3 distinct roles in PostgreSQL: `pipeline_writer`, `analyst_reader`, and `compliance_officer`.
- [ ] Assign least-privilege `SELECT`, `INSERT`, `UPDATE` permissions per role.
- [ ] Verify that an `analyst_reader` account cannot execute `DROP TABLE` or mutate data.

## Completion Criteria
- [ ] Compare architectural trade-offs between RBAC and ABAC.
- [ ] Implement an RBAC role hierarchy in PostgreSQL or Snowflake.
- [ ] Enforce schema-level and table-level access boundaries.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 | RBAC testing | Yes (Docker) | Yes | `docker start de-postgres` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### RBAC Setup in PostgreSQL
```sql
CREATE ROLE read_only_analyst;
GRANT CONNECT ON DATABASE warehouse TO read_only_analyst;
GRANT USAGE ON SCHEMA marts TO read_only_analyst;
GRANT SELECT ON ALL TABLES IN SCHEMA marts TO read_only_analyst;
ALTER DEFAULT PRIVILEGES IN SCHEMA marts GRANT SELECT ON TABLES TO read_only_analyst;
```

## Related Lessons
- Prerequisites: [[CLD-01 - AWS IAM Security]]
- Next Lesson: [[GOV-02 - Column Masking and Row-Level Security]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
