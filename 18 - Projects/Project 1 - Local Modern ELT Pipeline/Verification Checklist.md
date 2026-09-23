---
id: PRJ-01
name: Verification Checklist - Local Modern ELT Pipeline
aliases:
  - PRJ-01 Verification
---

# ✅ PRJ-01 Verification Checklist

- [ ] Docker Compose boots PostgreSQL 16 and Metabase cleanly without port conflicts (`docker compose up -d`).
- [ ] Python extractor fetches delta records idempotently using `updated_at` timestamps without duplicating keys.
- [ ] DuckDB database file is populated and queryable via DuckDB CLI (`duckdb retail.duckdb`).
- [ ] `dbt build` executes staging, intermediate, and mart models with 100% passing tests.
- [ ] Custom singular SQL test asserting `order_total = SUM(line_item_amount) + tax` passes with zero rows returned.
- [ ] SCD Type 2 customer table accurately creates new validity records upon upstream address update.
- [ ] Metabase connects to DuckDB and renders a 4-card revenue dashboard.
