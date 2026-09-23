---
title: Phase 4 - Cloud, DevOps & Reliability Engineering
phase: Phase 4
duration: Months 9–10 (8 Weeks)
aliases:
  - Phase 4
  - Phase 4 - Cloud & DevOps
---

# ☁️ Phase 4: Cloud, DevOps & Reliability Engineering

## Overview
Phase 4 elevates pipelines into production-grade cloud infrastructure. You will manage AWS cloud data primitives (IAM, S3, Glue, Athena), provision infrastructure declaratively with Terraform, package portable environments in multi-stage Dockerfiles, automate testing and deployment with GitHub Actions CI/CD, enforce data quality contracts with Soda Core, and capture end-to-end lineage via OpenLineage and Marquez.

---

## 🎯 Target Capabilities
- Architect secure AWS data pipelines enforcing least-privilege IAM policies, S3 lifecycle transitions, and serverless Athena querying.
- Provision repeatable cloud infrastructure declaratively using modular, state-locked Terraform code (tested on LocalStack & AWS).
- Build lightweight, secure multi-stage Docker images for data tools and coordinate multi-container local clusters with Docker Compose.
- Automate CI/CD pipelines in GitHub Actions enforcing code formatting (`ruff`), strict typing (`mypy`), and unit testing (`pytest`).
- Implement Data Quality Gating and the 5 Pillars of Observability (freshness, volume, schema, distribution, lineage) using Soda Core.
- Capture column-level runtime lineage automatically across Spark and dbt using OpenLineage and visualize it in Marquez.
- Implement data governance controls: Role-Based Access Control (RBAC), Attribute-Based Access Control (ABAC), and column-level PII masking.

---

## 📚 Modules in Phase 4
- **Module 13: Cloud Infrastructure (AWS Focus)**
  - [[CLD-01 - AWS IAM Security]]
  - [[CLD-02 - Amazon S3 Storage Architecture]]
  - [[CLD-03 - Amazon Athena and Glue Catalog]]
  - [[CLD-04 - Amazon EMR Serverless Spark]]
  - [[CLD-05 - Serverless Compute and VPCs]]
  - [[CLD-06 - Cloud Cost Optimization]]
- **Module 14: DevOps & Infrastructure as Code**
  - [[OPS-01 - Docker Fundamentals]]
  - [[OPS-02 - Multi-Stage Dockerfiles]]
  - [[OPS-03 - Docker Compose Platforms]]
  - [[OPS-04 - Terraform Syntax and State]]
  - [[OPS-05 - Terraform Modular Architecture]]
  - [[OPS-06 - Remote State and Backend Locking]]
  - [[OPS-07 - GitHub Actions CI-CD]]
  - [[OPS-08 - Automated Testing in CI]]
- **Module 15: Data Reliability Engineering & Observability**
  - [[DAT-01 - The 5 Pillars of Observability]]
  - [[DAT-02 - Pipeline Testing with Soda Core]]
  - [[DAT-03 - Validation with Great Expectations]]
  - [[DAT-04 - Data Contracts]]
  - [[DAT-05 - OpenLineage and Marquez]]
  - [[DAT-06 - Anomaly Detection and Alerting]]
- **Module 16: Data Governance & Security Engineering**
  - [[GOV-01 - Access Control Models RBAC ABAC]]
  - [[GOV-02 - Column Masking and Row-Level Security]]
  - [[GOV-03 - Data Encryption at Rest and Transit]]
  - [[GOV-04 - Enterprise Governance Unity and Polaris]]
  - [[GOV-05 - Compliance Engineering and GDPR]]

---

## 🏆 Milestone Gate 4 Exit Criteria
- [ ] Deliver **[[Project 4 - Production Cloud Platform Terraform/README|Project 4: Production Cloud Data Platform]]** provisioned cleanly via Terraform with automated CI/CD.
- [ ] Sit and pass the **[[AWS Certified Data Engineer DEA-C01|AWS Certified Data Engineer - Associate (DEA-C01)]]** examination.
- [ ] Verify that an intentional schema drift fails the automated CI pipeline before deployment.
