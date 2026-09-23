---
id: PRJ-02
name: Architecture - Scalable Lakehouse Spark Iceberg
aliases:
  - PRJ-02 Architecture
---

# 🏛️ PRJ-02 Architecture: Scalable Financial Lakehouse

```mermaid
flowchart TD
    Raw["Raw Financial Events (JSON/Parquet)<br/>10GB Ingestion Stream"] --> Bronze["Bronze Tier (Iceberg)<br/>Raw Append-Only + Ingestion Metadata"]
    Bronze --> Spark["PySpark 4.0 Engine<br/>Deduplication, PII Hashing, Type Casting"]
    Spark --> Silver["Silver Tier (Iceberg)<br/>Conformed Ledger Transactions (ACID MERGE)"]
    Silver --> Aggregate["Aggregations & Modeling<br/>Hidden Partitioning by month(txn_date)"]
    Aggregate --> Gold["Gold Tier (Iceberg)<br/>Daily Account Balances & Fraud Aggregates"]
    Gold --> Engines["Trino / DuckDB SQL Engines<br/>Time-Travel Audits & Analytics"]
```

## Core Lakehouse Principles Demonstrated
- **ACID Transactions on Object Storage**: Apache Iceberg guarantees snapshot isolation on MinIO S3 API without locking or inconsistent reads.
- **Hidden Partitioning**: Partitioned by `month(transaction_date)` and bucketed by `account_id` without requiring consumer queries to know partition physical layout.
- **In-Place Schema Evolution**: Adding metadata fields without rewriting data files.
