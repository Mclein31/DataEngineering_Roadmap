---
title: Data Engineering Technical Interview Roadmap
aliases:
  - Interview Roadmap
---

# 🎯 Data Engineering Technical Interview Roadmap

Technical data engineering interviews test a hybrid profile: software engineering fundamentals, database systems internals, distributed data manipulation, cloud infrastructure, and distributed system design.

---

## 🧭 The 8 Core Interview Tracks

### 1. Python Live Coding Track
- **Core Topics**: Object-oriented design, protocol typing (`typing.Protocol`), custom decorators, generator streams, context managers.
- **Data Structures**: Custom generators for streaming multi-gigabyte files, dict/set comprehensions, manipulating deeply nested JSON.
- **In-Memory Wrangling**: GroupBy aggregations, windowing, and joins using Polars and native dictionary lookups.
- **Benchmark Challenge**: Write a robust, rate-limited, paginated API client that ingests data into Parquet using Polars in < 50 lines of code.
- **Resource**: [[Python Data Wrangling Coding Bank]].

### 2. Analytical SQL Track
- **Core Topics**: Three-valued logic (NULL handling), `HAVING` vs `WHERE`, conditional aggregation (`FILTER` / `CASE`).
- **Complex Joins**: Anti-joins (`NOT EXISTS`), self-joins, cross-joins for generating test grids.
- **Window Functions**: `ROW_NUMBER()` vs `DENSE_RANK()`, `LEAD`/`LAG` for MoM growth, sliding window frames (`ROWS BETWEEN 6 PRECEDING AND CURRENT ROW`).
- **Hierarchies**: Recursive CTEs for organizational rollups and graph traversals.
- **Benchmark Challenge**: Solve 50 high-frequency SQL interview problems under a strict 20-minute timer per query.
- **Resource**: [[50 High-Frequency SQL Drills]].

### 3. Database & Storage Internals Track
- **OLTP vs OLAP**: Slotted page storage vs columnar compressed layouts (Run-Length, Dictionary encoding).
- **ACID & Concurrency**: Write-Ahead Logging (WAL) mechanics, Multi-Version Concurrency Control (MVCC), transaction isolation anomalies.
- **Query Performance**: Reading `EXPLAIN (ANALYZE, BUFFERS)` outputs, B-Tree traversal mechanics, eliminating sequential scans.
- **Benchmark Challenge**: Whiteboard how a database engine executes a Hash Join (Build phase vs Probe phase) and what happens when hash tables spill to disk.
- **Resource**: [[Systems Internals Question Defense]].

### 4. Data Engineering Core & Modeling Track
- **ETL vs ELT**: Architectural tradeoffs, staging paradigms, compute decoupling.
- **Data Modeling**: Kimball dimensional star schemas, degenerate dimensions, Slowly Changing Dimensions (SCD Type 1, 2, and 3).
- **Medallion Pattern**: Defining the exact data hygiene and schema enforcement rules between Bronze, Silver, and Gold tiers.
- **Benchmark Challenge**: Design a complete Kimball star schema for a ride-sharing platform (trips fact, drivers dim, passengers dim, surge pricing).

### 5. Distributed Systems (Spark & Kafka) Track
- **Spark Mechanics**: Catalyst Optimizer phases, physical execution plans, Adaptive Query Execution (AQE), broadcast vs sort-merge joins.
- **Spark Tuning**: Identifying shuffle spill, mitigating data skew via key salting, tuning executor and driver memory allocations.
- **Kafka Architecture**: KRaft consensus, topic partitioning, consumer group rebalancing, offset commits, exactly-once semantics (EOS).
- **Benchmark Challenge**: Diagnose a Spark job failure that crashed with `OutOfMemoryError: Java heap space` during a join of skewed customer data.

### 6. Cloud & DevOps Track
- **Cloud Architecture**: Least-privilege IAM policies, S3 lifecycle rules, Athena query optimization, serverless compute execution.
- **DataOps**: Multi-stage Docker optimization, declarative Terraform provisioning, automated testing via GitHub Actions.
- **Observability**: Implementing the 5 pillars of observability (Freshness, Volume, Schema, Distribution, Lineage).
- **Benchmark Challenge**: Write a complete Terraform configuration provisioning an encrypted S3 bucket, an IAM policy, and a Glue catalog database.

### 7. Distributed System Design Track
- **5-Step Protocol**:
  1. Clarify functional & non-functional requirements (SLA, latency, throughput).
  2. Conduct capacity math (Events/sec * Event size -> MB/s -> Storage/year).
  3. High-level architecture (Ingestion -> Storage -> Transformation -> Serving).
  4. Deep-dive into partitioning, idempotency, failure recovery, and dead-letter queues.
  5. Security, observability, and cost governance.
- **Benchmark Challenge**: Architect a real-time clickstream ingestion engine handling 100,000 events/second with sub-minute analytical query latency.

### 8. Behavioral Track (STAR Method)
- **Production Outage / Silent Data Bug**: A silent schema drift broke downstream reporting; describe triage, hotfix, and long-term automated prevention.
- **Technical Disagreement**: Defending an architectural choice (e.g., DuckDB vs Spark) using benchmarks and cost calculations.
- **Performance Optimization**: How you improved a slow-running pipeline, reducing runtime or cloud spend by > 50%.
- **Resource**: [[Behavioral STAR Incident Stories]].
