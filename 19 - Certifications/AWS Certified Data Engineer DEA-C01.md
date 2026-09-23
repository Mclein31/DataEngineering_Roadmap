---
certification: AWS Certified Data Engineer - Associate
provider: Amazon Web Services (AWS)
current_status: ACTIVE (Standard 2026 DE Credential)
exam: DEA-C01
cost: 150 USD
aliases:
  - AWS Certified Data Engineer DEA-C01
  - DEA-C01
---

# ☁️ AWS Certified Data Engineer - Associate (DEA-C01)

## Overview
The AWS Certified Data Engineer - Associate (DEA-C01) validates core technical skills in data ingestion, transformation, store management, pipeline operations, and security governance across the AWS cloud ecosystem.

---

## 📋 Exam Specification
- **Certification**: AWS Certified Data Engineer - Associate
- **Provider**: Amazon Web Services (AWS)
- **Current Status**: **ACTIVE (Current Industry Standard)**
- **Exam Code**: DEA-C01
- **Prerequisites**: None official (Mastery of Phase 1 and Phase 4 recommended)
- **Recommended Experience**: 6–12 months hands-on experience with AWS data services
- **Cost**: $150 USD
- **Exam Format**: 65 multiple-choice or multiple-response questions
- **Duration**: 130 minutes
- **Passing Score**: 720 / 1000 (scaled score)
- **Renewal / Validity**: 3 years
- **Official URL**: [aws.amazon.com/certification/certified-data-engineer-associate/](https://aws.amazon.com/certification/certified-data-engineer-associate/)

---

## 📊 Exam Domains & Weightings

```text
Domain 1: Data Ingestion and Transformation (28%)
Domain 2: Data Store Management (26%)
Domain 3: Data Operations and Support (22%)
Domain 4: Data Security and Governance (24%)
```

### Domain 1: Data Ingestion and Transformation (28%)
- Ingestion mechanisms: Kinesis Data Streams vs Kinesis Data Firehose, AWS Glue streaming ETL, AWS Lambda batch extractors, AWS DMS (Database Migration Service).
- Transformation: AWS Glue Studio, Glue PySpark jobs, dynamic frames vs Spark DataFrames, partitioning, compression formats (Parquet with Snappy/ZSTD).

### Domain 2: Data Store Management (26%)
- Amazon S3: Storage tiers (Standard, Intelligent-Tiering, Glacier), lifecycle rules, server-side encryption (SSE-S3, SSE-KMS), bucket policies.
- Amazon Redshift: Cluster architecture, RA3 nodes, distribution styles (AUTO, KEY, EVEN, ALL), sort keys (COMPOUND, INTERLEAVED), Redshift Spectrum.
- Amazon Athena: Serverless querying, Glue Data Catalog partitions, partition projection, result set reuse, workgroups.

### Domain 3: Data Operations and Support (22%)
- Orchestration: AWS Step Functions vs Apache Airflow (Amazon MWAA).
- Monitoring: Amazon CloudWatch alarms, metrics, CloudTrail API audit logging, SNS alerts on pipeline failure.
- Troubleshooting: Glue out-of-memory errors, S3 503 SlowDown throttling, Athena query timeouts.

### Domain 4: Data Security and Governance (24%)
- Identity & Access: IAM least-privilege policies, service roles, temporary credentials via STS.
- Encryption: AWS KMS key rotation, envelope encryption, transit encryption via TLS.
- Governance: AWS Lake Formation (table and column-level access permissions), AWS Glue Data Catalog cross-account resource sharing.

---

## 🛠️ Free Preparation & Hands-On Labs
1. **Official AWS Skill Builder**: [Data Engineer Learning Plan](https://explore.skillbuilder.aws/learn/public-catalog) (Free tier access).
2. **Local Practice via LocalStack**: Emulate S3, IAM, Athena, and Glue locally without incurring AWS charges.
3. **Practice Exams**: Tutorials Dojo DEA-C01 practice exam suite.

---

## ⚠️ Cloud Cost Warning & Safety Checklist
> [!WARNING] Avoid Accidental Billing
> When conducting hands-on labs in a live AWS sandbox:
> - Set up a **$5 Billing Alarm** in CloudWatch before provisioning any service.
> - Terminate Redshift clusters, EMR clusters, and MWAA environments immediately after testing.
> - Never run full unpartitioned Athena scans on multi-gigabyte datasets.
