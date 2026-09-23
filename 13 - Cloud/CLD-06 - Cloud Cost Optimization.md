---
id: CLD-06
title: Cloud Cost Optimization
phase: Phase 4
module: Module 13: Cloud Infrastructure (AWS Focus)
aliases:
  - CLD-06
---

# CLD-06 - Cloud Cost Optimization

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement cloud cost governance: AWS Budgets, CloudWatch billing alerts, S3 storage class transitions, and Athena query caps.

## Concepts
- **The 4 Pillars of Cloud Cost Optimization**:
  1. *Storage Lifecycle*: Automated transitions to Intelligent-Tiering and Glacier.
  2. *Query Scans*: Partitioning and columnar compression reducing Athena scans by 90%+.
  3. *Compute Sizing*: Spot instances for fault-tolerant Spark batch jobs; serverless auto-termination.
  4. *Governance & Budgets*: Automated billing alarms and action-driven cost thresholds.
- **AWS Budgets & Cost Explorer**: Tracking daily burn rates and alerting when forecasted spend exceeds monthly budgets.
- **Athena Data Limits**: Configuring per-query and per-hour byte limits in Workgroups to kill runaway queries.

## Learning Resource
- **Title**: AWS Cloud Financial Management & Cost Optimization
- **Provider / Author**: Amazon Web Services
- **URL**: https://aws.amazon.com/aws-cost-management/
- **Type**: Official Documentation
- **Topic**: Cost Optimization, AWS Budgets, Billing Alerts
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Set up an AWS Budget alerting via email when spend exceeds $5.00 USD.
- [ ] Configure an Athena Workgroup with a "Per Query Data Limit" of 10GB.
- [ ] Audit S3 bucket costs and verify zero abandoned multipart uploads using S3 lifecycle rules.

## Completion Criteria
- [ ] Configure a $5.00 billing alert in AWS CloudWatch / Budgets.
- [ ] Enforce hard query scan limits in Amazon Athena.
- [ ] Identify and clean up orphaned cloud storage resources.

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
### AWS Billing Alarm Setup
```bash
aws cloudwatch put-metric-alarm   --alarm-name "MonthlySpendExceeds5Dollars"   --metric-name EstimatedCharges   --namespace AWS/Billing   --statistic Maximum   --period 21600   --threshold 5.0   --comparison-operator GreaterThanOrEqualToThreshold   --evaluation-periods 1
```

## Related Lessons
- Prerequisites: [[CLD-03 - Amazon Athena and Glue Catalog]]
- Next Lesson: [[OPS-01 - Docker Fundamentals]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
