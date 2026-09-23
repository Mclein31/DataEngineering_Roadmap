---
id: CLD-05
title: Serverless Compute and VPCs
phase: Phase 4
module: Module 13: Cloud Infrastructure (AWS Focus)
aliases:
  - CLD-05
---

# CLD-05 - Serverless Compute and VPCs

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Coordinate serverless extractors (AWS Lambda) inside isolated Virtual Private Clouds (VPCs) with private S3 endpoints.

## Concepts
- **AWS Lambda for Micro-ETL**: Event-driven serverless functions (max 15-minute execution, 10GB RAM) for lightweight API extractors and S3 event triggers.
- **VPC Networking**: Subnets (public vs private), route tables, Internet Gateways (IGW), and NAT Gateways.
- **VPC Gateway Endpoints for S3**: Routing traffic between VPC resources and S3 across the private AWS backbone without traversing the public internet or paying NAT Gateway egress fees!
- **Security Groups**: Stateful virtual firewalls restricting inbound and outbound database traffic.

## Learning Resource
- **Title**: AWS VPC Endpoints Documentation
- **Provider / Author**: Amazon Web Services
- **URL**: https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-s3.html
- **Type**: Official Documentation
- **Topic**: AWS VPC, S3 Endpoints, Lambda Networking
- **Difficulty**: Intermediate
- **Category**: ⭐ RECOMMENDED

## Practice
- [ ] Architect a private VPC topology with two private subnets and a database security group.
- [ ] Configure an S3 Gateway Endpoint to enable free, private S3 data transfer.
- [ ] Write a serverless Python Lambda function fetching data and writing to S3 upon event notification.

## Completion Criteria
- [ ] Explain why VPC S3 Gateway Endpoints eliminate costly NAT Gateway data transfer fees.
- [ ] Restrict database access strictly to pipeline subnets via Security Group rules.
- [ ] Deploy an event-triggered Lambda function.

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
### Private S3 VPC Endpoint
```text
[Lambda inside Private Subnet] 
            │
            └──> [S3 Gateway Endpoint] ──> [Amazon S3] (Private AWS Backbone, $0 NAT fee!)
```

## Related Lessons
- Prerequisites: [[LNX-06 - Networking Fundamentals for DE]], [[CLD-01 - AWS IAM Security]]
- Next Lesson: [[CLD-06 - Cloud Cost Optimization]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
