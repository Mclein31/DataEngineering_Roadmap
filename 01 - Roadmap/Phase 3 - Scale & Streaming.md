---
title: Phase 3 - Scale, Distributed Compute & Streaming
phase: Phase 3
duration: Months 6–8 (12 Weeks)
aliases:
  - Phase 3
  - Phase 3 - Scale & Streaming
---

# ⚡ Phase 3: Scale, Distributed Compute & Streaming

## Overview
Phase 3 shifts focus to massive-scale distributed compute and real-time event streaming. You will explore Apache Parquet internals, master modern Open Table Formats (Apache Iceberg), write distributed PySpark 4.0 batch and streaming pipelines, automate data-aware orchestrations in Apache Airflow 3.x, and stream high-throughput events via Apache Kafka 4.0 in pure KRaft mode.

---

## 🎯 Target Capabilities
- Understand columnar Parquet physical layouts (file metadata, row groups, dictionary encoding, Snappy/ZSTD compression).
- Master Open Table Formats: Apache Iceberg metadata hierarchies (catalog, metadata JSON, manifest lists, manifest files) and snapshot isolation.
- Execute ACID table mutations, schema evolutions, hidden partitioning, and time-travel rollback queries in Apache Iceberg.
- Master distributed compute with Apache Spark 4.0: Spark Connect, Catalyst optimizer, physical plans, shuffle partitions, and Adaptive Query Execution (AQE).
- Diagnose and eliminate Spark executor `OutOfMemoryError` crashes, shuffle disk spills, and join data skew using key salting.
- Orchestrate end-to-end data pipelines using Apache Airflow 3.x TaskFlow API and event-driven `@asset` data dependencies.
- Deploy Apache Kafka 4.0 clusters in pure KRaft mode without ZooKeeper; master partition leaders, consumer groups, offset commits, and exactly-once semantics (EOS).
- Stream events with sub-5-second latency using PySpark Structured Streaming and Confluent Schema Registry (Avro).

---

## 📚 Modules in Phase 3
- **Module 09: Modern Data Lakes & Open Table Formats**
  - [[LAK-01 - Object Storage Architecture]]
  - [[LAK-02 - Apache Parquet Internals]]
  - [[LAK-03 - Limitations of Traditional Lakes]]
  - [[LAK-04 - Open Table Format Paradigm]]
  - [[LAK-05 - Apache Iceberg Architecture]]
  - [[LAK-06 - Iceberg Hidden Partitioning]]
  - [[LAK-07 - Delta Lake and UniForm]]
  - [[LAK-08 - Open Table Catalogs]]
- **Module 10: Distributed Compute with Apache Spark 4.0**
  - [[SPK-01 - Spark 4 Cluster Architecture]]
  - [[SPK-02 - Spark Connect Architecture]]
  - [[SPK-03 - PySpark DataFrame Mechanics]]
  - [[SPK-04 - Catalyst Optimizer Deep Dive]]
  - [[SPK-05 - Spark SQL Internals]]
  - [[SPK-06 - Shuffling Mechanics]]
  - [[SPK-07 - Join Strategies in Spark]]
  - [[SPK-08 - Adaptive Query Execution]]
  - [[SPK-09 - Spark Unified Memory Management]]
  - [[SPK-10 - Diagnosing Spark OOM and Spills]]
  - [[SPK-11 - Data Skew Mitigation]]
  - [[SPK-12 - Spark Structured Streaming]]
- **Module 11: Workflow Orchestration with Airflow 3.x**
  - [[AIR-01 - Orchestration Principles]]
  - [[AIR-02 - Airflow 3 Architecture]]
  - [[AIR-03 - TaskFlow API and Dynamic DAGs]]
  - [[AIR-04 - Data-Aware Asset Scheduling]]
  - [[AIR-05 - Event-Driven Orchestration]]
  - [[AIR-06 - Connections and Secrets]]
  - [[AIR-07 - Resilient DAGs and Retries]]
  - [[AIR-08 - Distributed Executors]]
  - [[AIR-09 - Dagster Asset Alternative]]
- **Module 12: Real-Time Event Streaming with Kafka 4.0**
  - [[KFK-01 - Event-Driven Fundamentals]]
  - [[KFK-02 - Kafka 4 KRaft Consensus]]
  - [[KFK-03 - Broker Internals and Log Partitions]]
  - [[KFK-04 - Producer Mechanics and Idempotence]]
  - [[KFK-05 - Consumer Groups and Offsets]]
  - [[KFK-06 - Delivery Guarantees]]
  - [[KFK-07 - Schema Registry and Avro]]
  - [[KFK-08 - Change Data Capture Debezium]]
  - [[KFK-09 - Stream Processing Patterns]]

---

## 🏆 Milestone Gate 3 Exit Criteria
- [ ] Deliver **[[Project 2 - Scalable Lakehouse Spark Iceberg/README|Project 2: Scalable Financial Ledger Lakehouse]]** with PySpark 4.0 and Apache Iceberg on MinIO.
- [ ] Deliver **[[Project 3 - Real-Time Streaming Ingestion/README|Project 3: Real-Time Fleet Streaming & Telemetry Pipeline]]** with Kafka 4.0 KRaft and Spark Structured Streaming.
- [ ] Demonstrate zero consumer lag buildup and deterministic discard of records outside the 10-minute watermark.
