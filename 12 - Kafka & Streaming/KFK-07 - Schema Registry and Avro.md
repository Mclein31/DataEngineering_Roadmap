---
id: KFK-07
title: Schema Registry and Avro
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-07
---

# KFK-07 - Schema Registry and Avro

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Enforce strict schema governance and backwards compatibility across streaming microservices using Confluent Schema Registry and Apache Avro.

## Concepts
- **The Danger of Untyped JSON in Kafka**: Upstream producers adding/removing fields without warning, breaking downstream Spark/Flink pipelines (silent schema poisoning).
- **Apache Avro Binary Serialization**: Highly compact binary encoding without field names; requires a JSON schema to serialize and deserialize.
- **Confluent Schema Registry Architecture**: Centralized HTTP service storing versioned schemas. Producers register schemas; consumers fetch schemas by 4-byte Schema ID embedded in message headers.
- **Compatibility Modes**:
  - `BACKWARD`: New schema can read data written by previous schema (fields deleted or added with defaults).
  - `FORWARD`: Old schema can read data written by new schema.
  - `FULL`: Both backward and forward compatible.

## Learning Resource
- **Title**: Confluent Schema Registry Documentation
- **Provider / Author**: Confluent Inc.
- **URL**: https://docs.confluent.io/platform/current/schema-registry/index.html
- **Type**: Official Documentation
- **Topic**: Schema Registry, Avro, Compatibility Modes
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Deploy Confluent Schema Registry container connected to local Kafka 4.0.
- [ ] Define an Avro schema `order.avsc` for an e-commerce transaction.
- [ ] Write a Python producer serializing messages with `confluent_kafka.schema_registry.avro.AvroSerializer`.
- [ ] Attempt to produce a message with an incompatible schema and verify rejection by the Schema Registry.

## Completion Criteria
- [ ] Prevent schema drift using Schema Registry validation.
- [ ] Write Avro schemas with default values to support backwards compatibility.
- [ ] Serialize and deserialize binary Avro messages in Python.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Confluent Schema Registry (Docker) | Schema management | Yes | Yes | `confluentinc/cp-schema-registry` | https://docs.confluent.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Avro Schema Example (`order.avsc`)
```json
{
  "type": "record",
  "name": "OrderEvent",
  "namespace": "com.retail.events",
  "fields": [
    {"name": "order_id", "type": "string"},
    {"name": "customer_id", "type": "long"},
    {"name": "total_amount", "type": "double"},
    {"name": "discount", "type": ["null", "double"], "default": null}
  ]
}
```

## Related Lessons
- Prerequisites: [[KFK-04 - Producer Mechanics and Idempotence]]
- Next Lesson: [[KFK-08 - Change Data Capture Debezium]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
