---
id: SPK-02
title: Spark Connect Architecture
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-02
---

# SPK-02 - Spark Connect Architecture

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Leverage Spark Connect for thin-client, serverless remote PySpark execution without JVM dependency conflicts.

## Concepts
- **Spark Connect Protocol**: Built atop Protocol Buffers (protobuf) and gRPC, serializing DataFrame operations into an unresolved logical plan sent over the network.
- **Eliminating JVM Dependency Issues**: Python clients require zero local Java installation or JVM setup; all plan compilation occurs on the remote driver.
- **Client-Side Debugging & Tooling**: Seamless integration into standard Python linters (`ruff`), debuggers (pdb), and tests (`pytest`) without driver crashes killing the local session.

## Learning Resource
- **Title**: Apache Spark Documentation - Spark Connect Overview
- **Provider / Author**: Apache Software Foundation
- **URL**: https://spark.apache.org/docs/latest/spark-connect-overview.html
- **Type**: Official Documentation
- **Topic**: Spark Connect, gRPC, Remote Clients
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Start a local Spark Connect server: `sbin/start-connect-server.sh`.
- [ ] Connect a thin Python script using `from pyspark.sql import SparkSession; spark = SparkSession.builder.remote("sc://localhost").getOrCreate()`.
- [ ] Verify that DataFrame transformations execute remotely on the server.

## Completion Criteria
- [ ] Connect to a remote Spark cluster using the `sc://` Spark Connect connection URI.
- [ ] Explain how Protocol Buffers serialize DataFrame transformation plans over gRPC.
- [ ] Debug a PySpark script locally with native Python debuggers using Spark Connect.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Spark Connect client | Yes | Yes | `uv pip install pyspark[connect]==4.0.0` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Spark Connect Remote Connection
```python
from pyspark.sql import SparkSession

# Connect to remote Spark 4 cluster without local JVM dependencies
spark = (
    SparkSession.builder
    .remote("sc://cluster-endpoint:15002")
    .getOrCreate()
)
df = spark.read.table("gold.fct_orders")
print(df.count())
```

## Related Lessons
- Prerequisites: [[SPK-01 - Spark 4 Cluster Architecture]]
- Next Lesson: [[SPK-03 - PySpark DataFrame Mechanics]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
