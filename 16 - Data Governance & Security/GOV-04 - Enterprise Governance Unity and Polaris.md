---
id: GOV-04
title: Enterprise Governance Unity and Polaris
phase: Phase 4
module: Module 16: Data Governance & Security Engineering
aliases:
  - GOV-04
---

# GOV-04 - Enterprise Governance Unity and Polaris

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Evaluate centralized enterprise data governance platforms: Databricks Unity Catalog and Snowflake/Apache Polaris Catalog.

## Concepts
- **The Governance Fragmentation Problem**: Maintaining separate user permissions inside Postgres, Snowflake, AWS IAM, and Databricks leads to permission drift and security vulnerabilities.
- **Centralized Data Governance Engines**:
  - *Databricks Unity Catalog*: Unified three-level namespace (`catalog.schema.table`), centralized audit logging, column masking, and automated lineage.
  - *Apache Polaris (Incubating)*: Open-source Iceberg REST catalog providing centralized cross-engine RBAC and credential vending for multi-cloud architectures.
- **Credential Vending**: The catalog authenticates the user and generates temporary, scoped S3/cloud credentials granting access only to the authorized Parquet files.

## Learning Resource
- **Title**: Apache Polaris Catalog Documentation
- **Provider / Author**: Apache Software Foundation
- **URL**: https://polaris.apache.org/
- **Type**: Official Documentation
- **Topic**: Enterprise Governance, Unity Catalog, Polaris
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare access control architectures across AWS Lake Formation, Databricks Unity Catalog, and Apache Polaris.
- [ ] Walk through how credential vending prevents compute engines from having direct root access to S3 storage buckets.

## Completion Criteria
- [ ] Explain how centralized catalogs resolve cross-engine access control fragmentation.
- [ ] Describe the credential vending security workflow.
- [ ] Design an enterprise namespace hierarchy (`catalog.schema.table`).

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
### Credential Vending Flow
```text
Trino / Spark Engine ──(Requests table)──> Polaris / Unity Catalog
                                                    │ (Evaluates RBAC)
Trino / Spark Engine <──(Returns temp S3 token)────┘
       │
       └──(Reads Parquet directly from S3 using scoped token)──> S3 Storage
```

## Related Lessons
- Prerequisites: [[LAK-08 - Open Table Catalogs]], [[GOV-01 - Access Control Models RBAC ABAC]]
- Next Lesson: [[GOV-05 - Compliance Engineering and GDPR]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
