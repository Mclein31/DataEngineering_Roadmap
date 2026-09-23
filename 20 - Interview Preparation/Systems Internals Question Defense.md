---
title: Systems Internals Question Defense
aliases:
  - Systems Internals Question Defense
---

# 🧠 Systems & Storage Internals Interview Defense

Detailed engineering responses to the most difficult technical questions asked during senior and staff data engineering systems rounds.

---

## 1. Storage Engines: Row-Oriented (Postgres) vs Columnar (Parquet/DuckDB)

### The Question
*"Why is columnar storage 10x-100x faster for analytical queries, and why can't we use it for transactional OLTP workloads?"*

### The Defense
- **OLTP & Slotted Page Storage**:
  - Relational engines like PostgreSQL store data in 8KB disk pages organized as slotted page layouts. Each page contains a line pointer array growing downward and tuple data growing upward.
  - When an application executes `INSERT INTO orders VALUES (...)`, the database writes the entire tuple contiguously into a single page and records the transaction in the Write-Ahead Log (WAL).
  - This design allows sub-millisecond point lookups and single-row mutations, but analytical queries (`SELECT AVG(amount) FROM orders`) must read every single 8KB page from disk into shared buffers, wasting 95% of memory bandwidth discarding irrelevant columns.
- **OLAP & Columnar Formats**:
  - Columnar engines (DuckDB, ClickHouse, Parquet) store column values contiguously in chunks (Row Groups).
  - **Vectorized Execution**: The CPU evaluates operations in tight vectorized SIMD loops (AVX-512) directly over contiguous memory arrays.
  - **Columnar Compression**: Homogeneous data types compress drastically better using Run-Length Encoding (RLE) and Dictionary Encoding.
  - **I/O Pruning**: Analytical queries reading only 2 columns read only those exact column byte offsets from disk, reducing I/O by orders of magnitude.
  - *Why not for OLTP*: Appending or updating a single row requires mutating every single separate column chunk across disk, introducing catastrophic write amplification.

---

## 2. Distributed Compute: Spark Catalyst & Adaptive Query Execution (AQE)

### The Question
*"Walk me through how Spark optimizes a DataFrame transformation and how AQE prevents shuffle spills at runtime."*

### The Defense
1. **Unresolved Logical Plan**: Spark validates syntax and ensures table and column names exist against the Catalog.
2. **Analyzed Logical Plan**: Data types and schema definitions are resolved.
3. **Optimized Logical Plan (Catalyst Rule-Based)**: Pushdown predicates (`filter` moved before `join`), column pruning (projecting only required fields), and constant folding.
4. **Physical Planning & Cost-Based Model**: Evaluates join strategies (Broadcast Hash Join vs Sort-Merge Join).
5. **Adaptive Query Execution (AQE)**:
   - In Spark 3.x and 4.0, AQE re-optimizes physical query plans *between shuffle stages* based on runtime statistics.
   - **Coalescing Shuffle Partitions**: Merges tiny post-shuffle partitions into fewer optimal-sized partitions (target ~64MB).
   - **Switching Join Strategies**: If a join table was estimated at 50MB but dynamically filtered down to 8MB at runtime, AQE converts a Sort-Merge Join into a Broadcast Hash Join dynamically, eliminating shuffle stages entirely.
   - **Mitigating Skew Joins**: Automatically splits oversized skewed partitions into sub-partitions.

---

## 3. Streaming Consensus: Apache Kafka 4.0 KRaft vs ZooKeeper

### The Question
*"Why did Apache Kafka eliminate ZooKeeper, and how does the KRaft metadata quorum work?"*

### The Defense
- **ZooKeeper Limitations**:
  - Previously, metadata was stored in ZooKeeper while data was stored on brokers.
  - Changes required broker-ZooKeeper synchronization; controller failover took tens of seconds as the new controller had to fetch and deserialize thousands of partition metadata states from ZooKeeper.
- **KRaft (Kafka Raft Metadata Mode)**:
  - In Kafka 4.0, metadata is treated as an internal, replicated Kafka event log (`@metadata` topic).
  - A quorum of dedicated controller nodes uses the Raft consensus protocol to elect an active metadata leader.
  - When metadata changes occur (topic created, partition reassigned), the active controller writes a record directly to the metadata log. Broker nodes replicate this log and hold hot, in-memory state machines.
  - Failover is near-instantaneous (sub-second) because follower controllers already possess the exact replicated state.
