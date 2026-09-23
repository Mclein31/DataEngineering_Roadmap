---
id: OPS-06
title: Remote State and Backend Locking
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-06
---

# OPS-06 - Remote State and Backend Locking

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Configure remote Terraform state storage in Amazon S3 with state locking via Amazon DynamoDB to prevent concurrent pipeline corruption.

## Concepts
- **The Local State Risk**: Committing `terraform.tfstate` to Git exposes plain-text secrets and causes state divergences across distributed engineering teams.
- **Remote State Storage (S3 Backend)**: Storing the central state file in an encrypted, versioned S3 bucket.
- **State Locking (DynamoDB)**: Acquiring an exclusive lock before running `plan` or `apply` to prevent concurrent team members or CI runners from overwriting state simultaneously.
- **State Migration**: Migrating existing local state to remote backend using `terraform init -migrate-state`.

## Learning Resource
- **Title**: Terraform Documentation - S3 Backend
- **Provider / Author**: HashiCorp
- **URL**: https://developer.hashicorp.com/terraform/language/settings/backends/s3
- **Type**: Official Documentation
- **Topic**: Remote State, State Locking, DynamoDB Backend
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Provision an S3 bucket for state storage and a DynamoDB table with `LockID` primary key.
- [ ] Configure the `backend "s3"` block in Terraform.
- [ ] Run `terraform init` to migrate local state to S3; observe the lock acquisition during `terraform apply`.

## Completion Criteria
- [ ] Configure remote state storage in S3 with server-side encryption enabled.
- [ ] Prevent concurrent deployment collisions using DynamoDB state locking.
- [ ] Explain why state files must never be checked into Git repositories.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Terraform | Backend locking | Yes | Yes | `brew install hashicorp/tap/terraform` | https://developer.hashicorp.com/terraform |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### S3 Backend Configuration Block
```hcl
terraform {
  backend "s3" {
    bucket         = "company-tfstate-storage"
    key            = "data-platform/prod.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-state-locks"
    encrypt        = true
  }
}
```

## Related Lessons
- Prerequisites: [[OPS-05 - Terraform Modular Architecture]]
- Next Lesson: [[OPS-07 - GitHub Actions CI-CD]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
