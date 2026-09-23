---
id: PRJ-03
name: Verification Checklist - Real-Time Fleet Streaming
aliases:
  - PRJ-03 Verification
---

# ✅ PRJ-03 Verification Checklist

- [ ] Kafka 4.0 cluster runs in KRaft mode with zero ZooKeeper containers.
- [ ] Schema Registry validates incoming Avro payloads and rejects invalid schemas.
- [ ] PySpark Structured Streaming consumer processes tumbling windows with 10-minute watermarking.
- [ ] Speed violations (>80 MPH) sink to TimescaleDB within 5 seconds.
- [ ] Grafana dashboard displays real-time fleet velocity without memory leak or consumer lag buildup over 15 minutes.
