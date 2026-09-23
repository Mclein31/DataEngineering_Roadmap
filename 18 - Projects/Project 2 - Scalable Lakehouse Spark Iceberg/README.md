---
id: PRJ-02
name: Project 2: Scalable Lakehouse Spark Iceberg
aliases:
  - PRJ-02
  - PRJ-02 Spec
  - PRJ-02 README
  - Project 2 - Scalable Lakehouse Spark Iceberg/README
  - 18 - Projects/Project 2 - Scalable Lakehouse Spark Iceberg/README
---

# PRJ-02: Scalable Financial Ledger Lakehouse

## 📌 Executive Summary
A distributed Lakehouse architecture processing semi-structured financial ledger and market transaction records using **PySpark 4.0** and **Apache Iceberg** open table format backed by **MinIO** object storage. Implements full Medallion Architecture (Bronze -> Silver -> Gold), ACID transactions, hidden partitioning, schema evolution, and time-travel audit queries.

---

## 🚀 Quickstart & Reproduction Guide (macOS)
```bash
# Start MinIO, Nessie/REST Catalog, and Spark cluster
docker compose up -d

# Verify MinIO console is accessible at http://localhost:9001
curl -I http://localhost:9000/minio/health/live

# Submit PySpark Lakehouse pipeline
spark-submit \
  --master local[*] \
  --packages org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.5.0 \
  src/lakehouse_pipeline.py
```
