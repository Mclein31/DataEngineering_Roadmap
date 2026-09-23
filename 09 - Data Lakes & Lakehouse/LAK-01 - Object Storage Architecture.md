---
id: LAK-01
title: Object Storage Architecture
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-01
---

# LAK-01 - Object Storage Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand the architecture of cloud object storage (Amazon S3, MinIO): flat key-value namespace, consistency models, and multi-part uploads.

## Concepts
- **Object Storage vs POSIX Filesystems**: Flat namespace; directories are an optical illusion created by forward slashes `/` in object keys. No rename operations (renaming a prefix copies every single object).
- **Strong Read-After-Write Consistency**: S3's 2020 consistency upgrade eliminating eventual consistency anomalies for `PUT` and `DELETE`.
- **Multipart Uploads**: Chunking files > 100MB into parallel 5MB–5GB parts for high-throughput uploads and automatic retry resilience.
- **Prefix Throttling Limits**: S3 partition request limits (3,500 PUT/POST/DELETE and 5,500 GET requests per second per prefix).

## Learning Resource
- **Title**: Fundamentals of Data Engineering (Chapter 4: Storage)
- **Provider / Author**: Joe Reis & Matt Housley (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fundamentals-of-data/9781098108298/
- **Type**: Textbook
- **Topic**: Object Storage Architecture, S3 Mechanics
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Launch local MinIO container: `docker run -d -p 9000:9000 -p 9001:9001 --name local-minio minio/minio server /data --console-address ":9001"`.
- [ ] Connect via Python `boto3` or MinIO Client (`mc`) and create a bucket `lakehouse-raw`.
- [ ] Upload a multi-part file and inspect prefix request metrics.

## Completion Criteria
- [ ] Explain why renaming a directory in object storage has $O(N)$ network cost.
- [ ] Configure and upload data using multipart upload APIs.
- [ ] Describe how S3 partitions request traffic across key prefixes.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| MinIO (Docker) | Local S3 API compatible storage | Yes (Docker) | Yes | `docker run -p 9000:9000 minio/minio server /data` | https://min.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Direct Parquet/Iceberg querying | Yes | Yes | `brew install duckdb` |

## Notes
### S3 Prefix Mechanics
```text
bucket/raw/year=2026/month=09/data_01.parquet  <-- Prefix is "raw/year=2026/month=09/"
Each unique prefix provides up to 5,500 GET requests/second.
```

## Related Lessons
- Prerequisites: [[DW-06 - Warehouse Cost Governance]]
- Next Lesson: [[LAK-02 - Apache Parquet Internals]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
