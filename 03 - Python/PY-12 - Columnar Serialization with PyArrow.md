---
id: PY-12
title: Columnar Serialization with PyArrow
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-12
---

# PY-12 - Columnar Serialization with PyArrow

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Understand zero-copy memory representation, Arrow IPC, and fine-tuned Parquet writing with dictionary encoding and compression.

## Concepts
- **Apache Arrow In-Memory Format**: Standardized columnar contiguous memory layout allowing zero-copy sharing across runtimes.
- **PyArrow Tables & Schemas**: Defining explicit field datatypes (`pa.schema`), nullable flags, and metadata dictionaries.
- **Parquet File Physical Structure**: Header magic bytes, Row Groups, Column Chunks, Pages, and File Footer metadata.
- **Compression Algorithms**: Snappy (low CPU, moderate compression) vs ZSTD (high compression ratio, configurable compression levels 1–22).

## Learning Resource
- **Title**: Apache Arrow Python Documentation (PyArrow)
- **Provider / Author**: Apache Software Foundation
- **URL**: https://arrow.apache.org/docs/python/
- **Type**: Official Documentation
- **Topic**: Columnar In-Memory, Parquet Serialization
- **Difficulty**: Advanced
- **Category**: ⭐ RECOMMENDED

## Practice
- [ ] Install PyArrow: `uv add pyarrow`.
- [ ] Convert a dataset into a `pyarrow.Table` with strict schema typing.
- [ ] Write the table to Parquet comparing file sizes across: uncompressed, Snappy, and ZSTD level 7.
- [ ] Inspect row group metadata using `pyarrow.parquet.read_metadata()`.

## Completion Criteria
- [ ] Compare disk footprints of the same dataset stored in CSV vs Snappy Parquet vs ZSTD Parquet.
- [ ] Explain how dictionary encoding reduces storage footprint on low-cardinality string columns.
- [ ] Inspect row groups and column statistics inside a Parquet file footer using PyArrow.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| PyArrow | Columnar memory and Parquet serialization | Yes (Native) | Yes | `uv add pyarrow` | https://arrow.apache.org/docs/python/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### PyArrow Parquet Writing
```python
import pyarrow as pa
import pyarrow.parquet as pq

schema = pa.schema([
    ("id", pa.int64(), False),
    ("category", pa.string(), True),
    ("price", pa.float64(), False)
])
table = pa.Table.from_arrays([...], schema=schema)
pq.write_table(table, "output.parquet", compression="zstd", compression_level=7)
```

## Related Lessons
- Prerequisites: [[PY-11 - Vectorized Processing with Polars]]
- Next Lesson: [[PY-13 - Unit Testing with pytest]]
- Phase Overview: [[Phase 1 - Foundations]]
