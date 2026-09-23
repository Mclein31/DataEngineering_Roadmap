---
id: LAK-02
title: Apache Parquet Internals
phase: Phase 3
module: Module 09: Modern Data Lakes & Open Table Formats
aliases:
  - LAK-02
---

# LAK-02 - Apache Parquet Internals

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Deeply inspect the binary structure of Apache Parquet: Row Groups, Column Chunks, Pages, Dictionary Encoding, and Thrift metadata footers.

## Concepts
- **Parquet Physical Layout**:
  - `Magic Number`: 4 bytes (`PAR1`) at beginning and end of file.
  - `Row Group`: Horizontal partitioning of rows (default 128MB to 512MB).
  - `Column Chunk`: The data for a specific column within a row group.
  - `Page`: The atomic unit of compression and encoding (default ~1MB). Data pages and dictionary pages.
  - `File Footer (Thrift)`: Contains file metadata, schema, and column statistics (min, max, null count).
- **Encoding Algorithms**: Plain, Dictionary Encoding, Run-Length Encoding (RLE), Bit-Packing, Delta Encoding.
- **Statistics & Predicate Pushdown**: The query engine reads the footer metadata first; if `min > target` or `max < target`, it skips reading the entire row group!

## Learning Resource
- **Title**: Apache Parquet Official Format Specification
- **Provider / Author**: Apache Software Foundation
- **URL**: https://parquet.apache.org/docs/file-format/
- **Type**: Official Documentation
- **Topic**: Parquet Internals, Encodings, Row Groups
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Generate a synthetic Parquet file containing sorted timestamps.
- [ ] Use `pyarrow.parquet.read_metadata()` to inspect row group count, column stats (min/max), and total byte size.
- [ ] Demonstrate predicate pushdown by querying the file in DuckDB with a filter, verifying row group skipping in `EXPLAIN`.

## Completion Criteria
- [ ] Inspect row group metadata and column min/max statistics programmatically using PyArrow.
- [ ] Explain how footer statistics enable predicate pushdown and disk block skipping.
- [ ] Articulate the trade-offs of setting row group sizes (e.g. 128MB vs 1GB).

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PyArrow & Python 3.12+ | Parquet metadata inspection | Yes | Yes | `uv pip install pyarrow` | https://arrow.apache.org/docs/python/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| DuckDB CLI | Direct Parquet/Iceberg querying | Yes | Yes | `brew install duckdb` |

## Notes
### Parquet File Layout Diagram
```text
4-byte Magic Number ("PAR1")
  ┌────────────────────────────────────────────────────────┐
  │ Row Group 1 (128MB)                                   │
  │   Column Chunk 1 (id)        [Data Pages & Dict Page]  │
  │   Column Chunk 2 (timestamp) [Data Pages]              │
  │   Column Chunk 3 (amount)    [Data Pages]              │
  ├────────────────────────────────────────────────────────┤
  │ Row Group 2 (128MB)                                   │
  │   ...                                                  │
  ├────────────────────────────────────────────────────────┤
  │ File Footer (Thrift Metadata)                          │
  │   - Schema                                             │
  │   - Row Group Metadata (Byte offsets, min/max stats)   │
  └────────────────────────────────────────────────────────┘
4-byte Magic Number ("PAR1")
```

## Related Lessons
- Prerequisites: [[PY-12 - Columnar Serialization with PyArrow]]
- Next Lesson: [[LAK-03 - Limitations of Traditional Lakes]]
- Phase Overview: [[Phase 3 - Scale & Streaming]]
