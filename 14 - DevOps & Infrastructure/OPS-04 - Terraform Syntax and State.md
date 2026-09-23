---
id: OPS-04
title: Terraform Syntax and State
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-04
---

# OPS-04 - Terraform Syntax and State

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Provision cloud infrastructure declaratively using HashiCorp Terraform syntax, resources, variables, and state management.

## Concepts
- **Infrastructure as Code (IaC) Principles**: Declarative configuration (`desired state`) vs imperative scripts (`step-by-step commands`). Version control, reproducibility, and zero manual clicks.
- **HashiCorp Configuration Language (HCL)**: Blocks (`provider`, `resource`, `variable`, `output`, `data`).
- **The Terraform Execution Lifecycle**:
  - `terraform init`: Initializes working directory and downloads provider plugins (AWS, LocalStack).
  - `terraform plan`: Generates execution plan comparing desired state against actual cloud state.
  - `terraform apply`: Provisions or updates resources to reach desired state.
  - `terraform destroy`: Safely tears down all tracked infrastructure.
- **The State File (`terraform.tfstate`)**: Maps declared resources to real-world cloud IDs; the source of truth for Terraform.

## Learning Resource
- **Title**: DataTalksClub Data Engineering Zoomcamp - Module 1: Terraform
- **Provider / Author**: Alexey Grigorev et al.
- **URL**: https://github.com/DataTalksClub/data-engineering-zoomcamp
- **Type**: Free Open-Source Course
- **Topic**: Terraform, IaC, HCL, State Management
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install Terraform: `brew install hashicorp/tap/terraform`.
- [ ] Configure `main.tf` with the AWS provider pointed to LocalStack (`http://localhost:4566`).
- [ ] Write Terraform code declaring an S3 bucket and an S3 bucket versioning resource.
- [ ] Run `terraform init`, `terraform plan`, and `terraform apply -auto-approve`.

## Completion Criteria
- [ ] Provision cloud storage resources declaratively via `terraform apply`.
- [ ] Inspect the generated `terraform.tfstate` file.
- [ ] Destroy all created resources cleanly via `terraform destroy`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Terraform | Infrastructure as Code | Yes (Native) | Yes | `brew install hashicorp/tap/terraform` | https://developer.hashicorp.com/terraform |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Basic Terraform HCL Configuration
```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
}

provider "aws" {
  region                      = "us-east-1"
  skip_credentials_validation = true
  skip_requesting_account_id  = true
  endpoints {
    s3 = "http://localhost:4566"
  }
}

resource "aws_s3_bucket" "lakehouse_raw" {
  bucket = "company-lakehouse-raw-dev"
}
```

## Related Lessons
- Prerequisites: [[CLD-01 - AWS IAM Security]]
- Next Lesson: [[OPS-05 - Terraform Modular Architecture]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
