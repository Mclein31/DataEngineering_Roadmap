---
id: SPK-12
title: Spark Structured Streaming
phase: Phase 3
module: Module 10: Distributed Compute with Apache Spark 4.0
aliases:
  - SPK-12
---

# SPK-12 - Spark Structured Streaming

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build fault-tolerant, event-driven stream processing pipelines with watermarking, windowing, and checkpointing using PySpark Structured Streaming.

## Concepts
- **Structured Streaming Engine**: Stream-as-an-unbounded-table model; micro-batch processing engine processing incoming records with sub-second latency.
- **Watermarking (`withWatermark`)**: Handling late-arriving events and bounding state store memory by defining an allowed lateness threshold.
- **Windowed Aggregations**: Tumbling (non-overlapping) vs Sliding (overlapping) time windows.
- **Output Modes**:
  - `Append`: Only new rows added to the result table are output (required for watermarked aggregations).
  - `Update`: Only rows updated since last micro-batch are output.
  - `Complete`: Entire updated result table output every batch.
- **Checkpointing**: Persisting write-ahead logs and state store offsets to cloud object storage for exactly-once recovery.

## Learning Resource
- **Title**: Learning Spark (2nd Edition) - Chapter 8: Structured Streaming
- **Provider / Author**: Jules S. Damji et al. (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/learning-spark-2nd/9781492050032/
- **Type**: Textbook
- **Topic**: Structured Streaming, Watermarks, Sinks
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a local streaming source reading mock JSON files arriving in a directory via `readStream`.
- [ ] Implement a 5-minute tumbling window with a 10-minute watermark on `event_time`.
- [ ] Configure `writeStream` sinking aggregated metrics to Parquet with a persistent checkpoint directory.

## Completion Criteria
- [ ] Configure watermarking to discard out-of-order records arriving outside the threshold.
- [ ] Explain how checkpoint directories guarantee exactly-once stream processing across crashes.
- [ ] Select appropriate output modes (Append vs Update vs Complete).

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PySpark 4.0 | Stream processing | Yes | Yes | `uv pip install pyspark` | https://spark.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| Java JDK 17 (OpenJDK) | Required JVM runtime for local Spark | Yes | Yes | `brew install openjdk@17` |

## Notes
### Structured Streaming Pipeline
```python
stream_df = (
    spark.readStream
    .format("parquet")
    .schema(sensor_schema)
    .load("data/stream_input/")
)

aggregated_df = (
    stream_df
    .withWatermark("timestamp", "10 minutes")
    .groupBy(F.window("timestamp", "5 minutes"), "sensor_id")
    .agg(F.avg("temperature").alias("avg_temp"))
)

query = (
    aggregated_df.writeStream
    .outputMode("append")
    .format("parquet")
    .option("checkpointLocation", "data/checkpoints/sensors/")
    .option("path", "data/stream_output/")
    .start()
)
query.awaitTermination()
```

## Related Lessons
- Prerequisites: [[SPK-03 - PySpark DataFrame Mechanics]]
- Next Lesson: [[AIR-01 - Orchestration Principles]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
