---
id: GOV-03
title: Data Encryption at Rest and Transit
phase: Phase 4
module: Module 16: Data Governance & Security Engineering
aliases:
  - GOV-03
---

# GOV-03 - Data Encryption at Rest and Transit

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement enterprise cryptographic standards: Transport Layer Security (TLS/SSL) in transit and envelope encryption at rest.

## Concepts
- **Encryption in Transit (TLS 1.3)**: Enforcing encrypted communication across all database ports, Kafka brokers, and API endpoints. Certificate validation and cipher suites.
- **Encryption at Rest**: Encrypting data on physical disks (S3 buckets, database tablespaces, Kafka log segments).
- **Envelope Encryption & AWS KMS**:
  - Encrypting data with a unique Data Encryption Key (DEK).
  - Encrypting the DEK with a master Key Encryption Key (KEK) stored inside Hardware Security Modules (HSMs).
- **Key Rotation Policies**: Automating annual cryptographic key rotation without re-encrypting historical data files.

## Learning Resource
- **Title**: AWS Key Management Service (KMS) Cryptographic Details
- **Provider / Author**: Amazon Web Services
- **URL**: https://docs.aws.amazon.com/kms/latest/developerguide/concepts.html
- **Type**: Official Documentation
- **Topic**: KMS, Envelope Encryption, Cryptography
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure PostgreSQL to enforce SSL-only connections (`ssl = on`).
- [ ] Review envelope encryption mechanics and explain why KMS uses DEKs instead of directly encrypting gigabytes of data.
- [ ] Encrypt an S3 bucket in LocalStack using a customer-managed KMS key.

## Completion Criteria
- [ ] Explain the cryptographic workflow of envelope encryption.
- [ ] Enforce SSL/TLS connections on database connection strings (`sslmode=require`).
- [ ] Differentiate between SSE-S3 and SSE-KMS.

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
### Envelope Encryption Mechanics
```text
Customer Data (Gigabytes) ──[Encrypted via DEK]──> Encrypted Data File
                                                        ▲
KMS Master Key (KEK) ───────[Encrypted DEK]─────────────┘
```

## Related Lessons
- Prerequisites: [[CLD-02 - Amazon S3 Storage Architecture]]
- Next Lesson: [[GOV-04 - Enterprise Governance Unity and Polaris]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
