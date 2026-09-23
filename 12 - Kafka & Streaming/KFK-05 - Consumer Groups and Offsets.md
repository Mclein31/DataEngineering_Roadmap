---
id: KFK-05
title: Consumer Groups and Offsets
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-05
---

# KFK-05 - Consumer Groups and Offsets

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Scale stream consumption across consumer groups, manage partition rebalancing, and track consumer lag.

## Concepts
- **Consumer Groups**: Pool of consumers cooperating to read partitions from a topic.
- **Partition Assignment Rule**: Each partition is consumed by *at most one* consumer within a consumer group. If consumers > partitions, extra consumers sit idle!
- **Offset Management (`__consumer_offsets`)**: Tracking consumer progress. Offset commits (`auto.commit` vs manual synchronous/asynchronous commits).
- **Consumer Rebalancing**: Reassigning partitions when consumers join, leave, or fail (Cooperative Sticky Rebalance protocol).
- **Consumer Lag**: The difference between the latest partition offset and the consumer's current offset; the primary health metric of a streaming pipeline.

## Learning Resource
- **Title**: Kafka: The Definitive Guide (2nd Edition) - Chapter 4: Kafka Consumers
- **Provider / Author**: Gwen Shapira et al. (Confluent)
- **URL**: https://www.confluent.io/resources/kafka-the-definitive-guide-2nd-edition/
- **Type**: Free Official eBook
- **Topic**: Consumer Groups, Offsets, Rebalancing
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a topic with 4 partitions.
- [ ] Spin up 2 consumer instances in the same consumer group and verify each reads 2 partitions.
- [ ] Launch a 3rd consumer and observe cooperative rebalancing in action.
- [ ] Inspect consumer lag using `kafka-consumer-groups.sh --describe --group order_processors`.

## Completion Criteria
- [ ] Scale consumers within a consumer group without dropping messages.
- [ ] Commit offsets manually after successful database persistence (`enable.auto.commit = false`).
- [ ] Monitor and alert on consumer lag buildup.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Apache Kafka (via Docker) | Consumer group management | Yes | Yes | `Docker Kafka` | https://kafka.apache.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Checking Consumer Lag via CLI
```bash
kafka-consumer-groups.sh   --bootstrap-server localhost:9092   --describe --group order_processors
# Output displays: TOPIC, PARTITION, CURRENT-OFFSET, LOG-END-OFFSET, LAG
```

## Related Lessons
- Prerequisites: [[KFK-04 - Producer Mechanics and Idempotence]]
- Next Lesson: [[KFK-06 - Delivery Guarantees]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
