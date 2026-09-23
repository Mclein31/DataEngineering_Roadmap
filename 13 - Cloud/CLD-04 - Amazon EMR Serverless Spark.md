---
id: CLD-04
title: Amazon EMR Serverless Spark
phase: Phase 4
module: Module 13: Cloud Infrastructure (AWS Focus)
aliases:
  - CLD-04
---

# CLD-04 - Amazon EMR Serverless Spark

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Execute distributed PySpark jobs on AWS without managing EC2 instances or cluster scaling using Amazon EMR Serverless.

## Concepts
- **Serverless Distributed Compute**: Eliminating EC2 provisioning, cluster resizing, and OS patching. EMR Serverless automatically provisions and scales driver and worker compute capacity.
- **Application Sizing & Worker Limits**: Configuring initial capacity, maximum capacity (`maximumCapacity`), and auto-stop timeouts to control costs.
- **Submitting Jobs via AWS CLI / SDK**: Submitting packaged PySpark scripts with virtual environments (`--conf spark.archives=...`).
- **Cost Monitoring**: Billing strictly for vCPU, memory, and storage resources consumed per second of job execution.

## Learning Resource
- **Title**: Amazon EMR Serverless User Guide
- **Provider / Author**: Amazon Web Services
- **URL**: https://docs.aws.amazon.com/emr/latest/EMR-Serverless-UserGuide/emr-serverless.html
- **Type**: Official Documentation
- **Topic**: EMR Serverless, PySpark Jobs, Cloud Compute
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Review EMR Serverless job submission parameters.
- [ ] Package a Python script and dependencies into a `.tar.gz` archive for cloud execution.
- [ ] Write a script triggering a job run via `aws emr-serverless start-job-run`.

## Completion Criteria
- [ ] Explain the cost and operational benefits of EMR Serverless over persistent EMR clusters.
- [ ] Package PySpark dependencies for serverless remote execution.
- [ ] Configure `maximumCapacity` limits to prevent runaway cluster auto-scaling.

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
### EMR Serverless Job Submission Command
```bash
aws emr-serverless start-job-run   --application-id $APP_ID   --execution-role-arn $ROLE_ARN   --job-driver '{
    "sparkSubmit": {
      "entryPoint": "s3://my-bucket/scripts/etl.py",
      "sparkSubmitParameters": "--conf spark.executor.cores=4 --conf spark.executor.memory=16g"
    }
  }'
```

## Related Lessons
- Prerequisites: [[SPK-01 - Spark 4 Cluster Architecture]], [[CLD-01 - AWS IAM Security]]
- Next Lesson: [[CLD-05 - Serverless Compute and VPCs]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
