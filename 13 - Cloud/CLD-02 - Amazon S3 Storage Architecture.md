---
id: CLD-02
title: Amazon S3 Storage Architecture
phase: Phase 4
module: Module 13: Cloud Infrastructure (AWS Focus)
aliases:
  - CLD-02
---

# CLD-02 - Amazon S3 Storage Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Design scalable, cost-effective Amazon S3 lakehouse storage tiers, lifecycle policies, and server-side encryption.

## Concepts
- **S3 Storage Classes**:
  - `S3 Standard`: High-frequency access, lowest latency.
  - `S3 Intelligent-Tiering`: Automatic cost optimization moving objects between frequent, infrequent, and archive access tiers based on usage patterns.
  - `S3 Glacier Flexible / Deep Archive`: Long-term cold data archive (retrieval times minutes to hours).
- **Lifecycle Configuration**: Transitioning raw files from Standard to Glacier after 90 days and expiring scratch partitions after 14 days.
- **Server-Side Encryption (SSE)**: SSE-S3 (managed keys) vs SSE-KMS (customer-managed KMS keys with audit trail).
- **Bucket Policies & Block Public Access**: Hard security constraints blocking all public read/write access.

## Learning Resource
- **Title**: Amazon S3 User Guide - Storage Classes & Lifecycle Management
- **Provider / Author**: Amazon Web Services
- **URL**: https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html
- **Type**: Official Documentation
- **Topic**: Amazon S3, Storage Classes, Lifecycles
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Configure S3 bucket in LocalStack or AWS with Block Public Access enabled.
- [ ] Define an S3 Lifecycle rule transitioning files under `raw/` to Glacier after 30 days.
- [ ] Upload an encrypted file using SSE-KMS via `aws s3 cp --sse aws:kms`.

## Completion Criteria
- [ ] Configure an automated S3 Lifecycle rule in JSON or Terraform.
- [ ] Articulate the cost savings of S3 Intelligent-Tiering for analytical lakehouses.
- [ ] Verify that public access is blocked at the account and bucket levels.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| AWS CLI | S3 configuration | Yes | Yes | `brew install awscli` | https://aws.amazon.com/cli/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### S3 Lifecycle JSON Rule
```json
{
  "Rules": [
    {
      "ID": "MoveRawToGlacier",
      "Filter": {"Prefix": "raw/"},
      "Status": "Enabled",
      "Transitions": [
        {"Days": 90, "StorageClass": "GLACIER"}
      ]
    }
  ]
}
```

## Related Lessons
- Prerequisites: [[CLD-01 - AWS IAM Security]]
- Next Lesson: [[CLD-03 - Amazon Athena and Glue Catalog]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
