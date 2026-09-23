---
id: DB-01
title: Row vs Columnar Storage
phase: Phase 2
module: Module 05: Database Internals & Storage Engines
aliases:
  - DB-01
---

# DB-01 - Row vs Columnar Storage

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand physical storage page layouts, row-oriented slotted pages, columnar block compression, and OLTP vs OLAP tradeoffs.

## Concepts
- **Slotted Page Architecture (OLTP)**: How PostgreSQL and MySQL InnoDB store contiguous records inside 8KB disk pages. Page headers, line pointers (ItemIds), free space, and tuple headers (`xmin`, `xmax`).
- **Columnar Format Architecture (OLAP)**: Contiguous in-memory and on-disk representation of homogenous columns.
- **Compression Mechanisms**: Run-Length Encoding (RLE), Bit-Packing, Dictionary Encoding, Frame of Reference (FOR).
- **SIMD Vectorization**: Processing arrays of integers/floats in single CPU cycles using AVX-512 vector registers.

## Learning Resource
- **Title**: Designing Data-Intensive Applications (Chapter 3: Storage and Retrieval)
- **Provider / Author**: Martin Kleppmann (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903117/
- **Type**: Textbook
- **Topic**: Storage Engines, Row vs Columnar Layouts
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Compare query performance on 10M rows in PostgreSQL vs DuckDB for `SELECT AVG(price), SUM(qty) FROM sales`.
- [ ] Measure disk space occupied by the same dataset in PostgreSQL vs Parquet format with ZSTD compression.
- [ ] Inspect row slotted page layout using PostgreSQL `pageinspect` extension.

## Completion Criteria
- [ ] Explain why columnar layouts allow orders-of-magnitude faster aggregations than row pages.
- [ ] Articulate write amplification in columnar formats for single-row OLTP transactions.
- [ ] Install and inspect an 8KB heap page using `SELECT * FROM page_header(get_raw_page('sales', 0));`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PostgreSQL 16 & DuckDB | Storage engine benchmarking | Yes | Yes | `brew install duckdb && docker run -p 5432:5432 postgres:16` | https://duckdb.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DBeaver Community | SQL query exploration | Yes | Yes | Universal free database GUI |

## Notes
### Storage Layout Comparison
```text
Row Storage (Postgres 8KB Page):
[Tuple 1: id, name, age, city][Tuple 2: id, name, age, city]...

Columnar Storage (DuckDB / Parquet Chunk):
[Col id: 1, 2, 3...][Col name: Alice, Bob...][Col age: 25, 30...][Col city: NY, LA...]
```

## Related Lessons
- Prerequisites: [[SQL-14 - Indexing Strategies and B-Trees]]
- Next Lesson: [[DB-02 - Write-Ahead Logging and Durability]]
- Phase Overview: [[Phase 2 - Storage & ELT]]
