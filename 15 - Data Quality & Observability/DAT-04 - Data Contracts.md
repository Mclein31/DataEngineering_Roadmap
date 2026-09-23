---
id: DAT-04
title: Data Contracts
phase: Phase 4
module: Module 15: Data Reliability Engineering & Observability
aliases:
  - DAT-04
---

# DAT-04 - Data Contracts

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement strict Data Contracts at producer-consumer ingestion boundaries using JSON Schema and Protobuf specifications.

## Concepts
- **What is a Data Contract?**: Formal agreement between software engineering producers (upstream microservices) and data consumers (data engineering/analytics).
- **Core Components of a Contract**:
  - *Schema*: Field names, types, constraints, descriptions.
  - *SLA & Semantics*: Expected update frequency, delivery latency, retention period.
  - *Security*: Classification level (Public, Internal, Confidential, Restricted/PII).
- **Contract Enforcement Points**: Validating payloads in CI before API releases; rejecting non-compliant payloads at ingestion gateways (routing to Dead Letter Queue).

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 5: Data Contracts)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Data Contracts, Schema Governance, SLIs/SLOs
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Author a formal Data Contract YAML specification for an e-commerce checkout service.
- [ ] Write a Python validator asserting incoming API batches conform 100% to the contract schema.
- [ ] Simulate an upstream microservice renaming a field and verify that the contract validation halts ingestion and alerts the owning team.

## Completion Criteria
- [ ] Define the 3 core pillars of an enterprise Data Contract (Schema, SLA, Security).
- [ ] Implement an automated Data Contract gate at an API ingestion gateway.
- [ ] Route contract-violating records to a Dead Letter Queue without crashing the pipeline.

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
### Data Contract Specification Example
```yaml
contract_version: "1.0.0"
dataset: "orders"
owner: "checkout-team@company.com"
sla:
  freshness_hours: 1
  uptime_pct: 99.9
schema:
  - name: order_id
    type: string
    required: true
    unique: true
  - name: total_amount
    type: numeric
    required: true
    bounds:
      min: 0.01
```

## Related Lessons
- Prerequisites: [[PY-03 - Data Validation with Pydantic]], [[DAT-01 - The 5 Pillars of Observability]]
- Next Lesson: [[DAT-05 - OpenLineage and Marquez]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
