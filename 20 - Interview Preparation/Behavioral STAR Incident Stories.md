---
title: Behavioral STAR Incident Stories
aliases:
  - Behavioral STAR Incident Stories
---

# 🎙️ Behavioral STAR Incident Stories for Data Engineers

These five production scenarios are structured using the **Situation, Task, Action, Result (STAR)** framework, highlighting technical leadership, root-cause triage, and data platform ownership.

---

## 🚨 Story 1: Production Outage / Silent Schema Drift

### Situation
A critical executive revenue dashboard displayed zero revenue for European orders on the first day of the fiscal quarter. Upstream microservices had updated their customer address payload from a flat string to a nested JSON object without notifying the data team.

### Task
Restore the executive pipeline immediately, identify why no alerts fired, and implement automated schema drift gating to prevent future occurrences.

### Action
1. **Triage**: Inspected Airflow task logs and detected that the Python extractor was catching schema errors and dropping records to avoid crashing the job.
2. **Hotfix**: Wrote a patch unnesting the address JSON field, backfilled the missed 14 hours of orders from S3 raw landing storage, and refreshed the analytical marts.
3. **Permanent Prevention**: Integrated Pydantic v2 validation models at the ingestion gateway. Configured Soda Core data contracts in CI/CD: any unexpected schema change automatically routes records to a Dead Letter Queue (DLQ) and sends high-priority PagerDuty alerts to the owning engineering team.

### Result
Downstream reports were restored within 45 minutes with zero lost transactions. The new schema contract framework caught three subsequent unannounced API breaking changes over the next six months.

---

## ⚡ Story 2: Performance Optimization & Cloud Cost Reduction

### Situation
A daily PySpark ETL job processing 2TB of user clickstream logs was consistently exceeding its 4-hour SLA, taking over 6.5 hours to finish and spilling hundreds of gigabytes to disk during join stages.

### Task
Optimize the PySpark pipeline to complete within the 2-hour SLA window while reducing compute cluster infrastructure spend.

### Action
1. **Diagnosis**: Inspected the Spark UI and identified extreme data skew on a join key (`user_id = NULL` and guest user sessions), causing a single executor task to run for 4 hours while all other executors sat idle.
2. **Key Salting**: Implemented key salting on the skewed join key and filtered out null identifiers prior to the join.
3. **AQE Tuning**: Enabled Spark Adaptive Query Execution (`spark.sql.adaptive.enabled = true`) and adjusted shuffle partitions from 200 to 1,200.

### Result
Runtime dropped from 6.5 hours to 42 minutes (an 89% speedup), completely eliminating disk spills. AWS EMR cluster sizing was reduced from 32 worker nodes to 12, saving over $4,200 monthly in cloud infrastructure.
