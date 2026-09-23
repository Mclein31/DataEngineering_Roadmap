---
id: PRJ-02
name: Verification Checklist - Scalable Lakehouse
aliases:
  - PRJ-02 Verification
---

# ✅ PRJ-02 Verification Checklist

- [ ] MinIO and Iceberg REST Catalog initialize cleanly via Docker Compose.
- [ ] Bronze Iceberg table ingests raw events without schema failure.
- [ ] Silver PySpark transformation executes an idempotent `MERGE INTO` handling late-arriving ledger updates.
- [ ] Column rename and new field addition verified without data corruption.
- [ ] Time-travel query successfully reads historical balances as of a specific snapshot ID.
