---
id: PRJ-05
name: Architecture - Converged Enterprise Lakehouse
aliases:
  - PRJ-05 Architecture
---

# 🏛️ PRJ-05 Architecture: Converged Enterprise Lakehouse

```mermaid
flowchart TD
    subgraph Ingestion["Dual Ingestion Tier"]
        Batch["Financial CSV Daily Batches<br/>(External APIs / SFTP)"]
        Stream["Real-Time Kafka 4.0 Streams<br/>(User Telemetry & Clicks)"]
    end

    subgraph StorageBronze["Bronze Storage Layer (Apache Iceberg)"]
        RawBatch["raw_financials (Append-Only)"]
        RawStream["raw_telemetry (Append-Only)"]
    end

    subgraph Orchestration["Orchestration Engine (Apache Airflow 3.x)"]
        AssetTrigger["@asset Data-Driven Scheduler<br/>Listens to Iceberg Snapshots"]
    end

    subgraph Processing["Distributed Compute & Cleansing"]
        SparkCleanser["PySpark 4.0 Cleanser<br/>PII Masking, Type Casting, Deduplication"]
    end

    subgraph StorageSilver["Silver Storage Layer (Apache Iceberg)"]
        SilverLedger["silver_ledger (ACID MERGE)"]
        SilverEvents["silver_events (Partitioned)"]
    end

    subgraph Modeling["Analytical Modeling (dbt-core)"]
        DbtMarts["dbt Gold Marts<br/>fct_financial_activity, dim_users_scd2"]
    end

    subgraph LineageGovernance["Lineage & Governance"]
        OL["OpenLineage Emission"]
        Marquez["Marquez Lineage UI<br/>Column-Level Dependency Graph"]
    end

    subgraph Serving["Serving Tier & BI"]
        Trino["Trino Distributed SQL Engine"]
        Dashboards["Superset / Metabase Dashboards"]
    end

    Batch --> RawBatch
    Stream --> RawStream
    RawBatch & RawStream --> AssetTrigger
    AssetTrigger --> SparkCleanser
    SparkCleanser --> SilverLedger & SilverEvents
    SilverLedger & SilverEvents --> DbtMarts
    SparkCleanser & DbtMarts -.->|Emit Lineage| OL
    OL --> Marquez
    DbtMarts --> Trino
    Trino --> Dashboards
```

## Architectural Decisions & Trade-Offs (ADRs)
1. **Convergence of Batch and Streaming**: Apache Iceberg serves as the single unified storage layer for both streaming Kafka append jobs and daily batch files, eliminating lambda architecture storage duplication.
2. **Airflow 3.x Asset-Centric Dependencies**: Instead of fragile cron intervals, tasks execute automatically as soon as upstream Iceberg snapshot metadata indicates new partition writes.
3. **OpenLineage Integration**: Both PySpark and dbt-core emit OpenLineage events, capturing end-to-end column-level transformations into Marquez without manual documentation.
