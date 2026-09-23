---
id: OPS-05
title: Terraform Modular Architecture
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-05
---

# OPS-05 - Terraform Modular Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build reusable, production-grade Terraform infrastructure modules with clear input variables, validation, and outputs.

## Concepts
- **Terraform Modules**: Packaging infrastructure into reusable, testable components (`modules/s3`, `modules/iam`, `modules/glue`).
- **Module Structure**: `main.tf` (resources), `variables.tf` (inputs and type validation), `outputs.tf` (exported ARNs and IDs).
- **Environment Segregation**: Reusing the same core modules across multiple environments (`dev`, `staging`, `prod`) by supplying different variable inputs (`dev.tfvars`, `prod.tfvars`).

## Learning Resource
- **Title**: Terraform Official Documentation - Creating Modules
- **Provider / Author**: HashiCorp
- **URL**: https://developer.hashicorp.com/terraform/language/modules/develop
- **Type**: Official Documentation
- **Topic**: Terraform Modules, Reusability, Parameterization
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a reusable module `modules/data_lake_bucket` that provisions an S3 bucket with encryption and lifecycle rules.
- [ ] Instantiate the module twice in `main.tf` to create `raw_bucket` and `curated_bucket`.
- [ ] Export the generated bucket ARNs in `outputs.tf`.

## Completion Criteria
- [ ] Create a reusable Terraform module conforming to standard file structure.
- [ ] Enforce variable type validation (`type = string`, `validation { ... }`).
- [ ] Instantiate the module cleanly across multiple target environments.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Terraform | Modular IaC | Yes | Yes | `brew install hashicorp/tap/terraform` | https://developer.hashicorp.com/terraform |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Module Directory Layout
```text
terraform/
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   └── terraform.tfvars
│   └── prod/
└── modules/
    ├── s3_bucket/
    │   ├── main.tf
    │   ├── variables.tf
    │   └── outputs.tf
    └── glue_database/
```

## Related Lessons
- Prerequisites: [[OPS-04 - Terraform Syntax and State]]
- Next Lesson: [[OPS-06 - Remote State and Backend Locking]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
