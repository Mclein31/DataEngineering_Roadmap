---
id: KFK-06
title: Delivery Guarantees
phase: Phase 3
module: Module 12: Real-Time Event Streaming with Kafka 4.0
aliases:
  - KFK-06
---

# KFK-06 - Delivery Guarantees

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Evaluate and implement delivery semantics: At-Most-Once, At-Least-Once, and Exactly-Once Semantics (EOS).

## Concepts
- **The 3 Delivery Semantics**:
  - *At-Most-Once*: Offsets committed before processing data. Crashes cause lost messages, but duplicates never occur.
  - *At-Least-Once (Standard)*: Offsets committed after processing data. Crashes cause replay of processed messages (duplicates possible).
  - *Exactly-Once Semantics (EOS)*: Every message affects downstream state exactly once, even during crashes.
- **Kafka Transactions (Transactional Producer)**: Atomic writes across multiple topic partitions and consumer offset commits via a two-phase commit protocol.
- **Downstream Idempotency**: Implementing idempotent sinks (e.g. `INSERT ... ON CONFLICT DO UPDATE` or unique keys) to achieve effective exactly-once processing with standard at-least-once consumers.

## Learning Resource
- **Title**: Kafka: The Definitive Guide (2nd Edition) - Reliable Data Delivery
- **Provider / Author**: Gwen Shapira et al. (Confluent)
- **URL**: https://www.confluent.io/resources/kafka-the-definitive-guide-2nd-edition/
- **Type**: Free Official eBook
- **Topic**: Delivery Guarantees, Exactly-Once, Transactions
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Implement an At-Least-Once consumer that commits offsets only after persisting records to PostgreSQL.
- [ ] Simulate a consumer crash immediately after database insert but before offset commit; verify duplicate processing on restart.
- [ ] Add an idempotent database constraint (`ON CONFLICT (txn_id) DO NOTHING`) to eliminate duplicate insertion.

## Completion Criteria
- [ ] Articulate the technical mechanisms of At-Most-Once, At-Least-Once, and Exactly-Once.
- [ ] Build an idempotent sink pattern in PostgreSQL handling duplicate consumer deliveries.
- [ ] Explain how Kafka transactional producers coordinate two-phase commits.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL & Kafka (Docker) | Idempotent sink testing | Yes | Yes | `Docker` | https://www.postgresql.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| kcat (formerly kafkacat) | Kafka CLI producer/consumer probe | Yes | Yes | `brew install kcat` |

## Notes
### Idempotent Consumer Pattern
```python
# Process message and commit only after DB transaction succeeds
for msg in consumer:
    record = json.loads(msg.value())
    cursor.execute('''
        INSERT INTO processed_events (event_id, payload) 
        VALUES (%s, %s) 
        ON CONFLICT (event_id) DO NOTHING;
    ''', (record['id'], json.dumps(record)))
    db_conn.commit()
    consumer.commit(msg)
```

## Related Lessons
- Prerequisites: [[KFK-05 - Consumer Groups and Offsets]]
- Next Lesson: [[KFK-07 - Schema Registry and Avro]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
