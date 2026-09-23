---
id: PY-11
title: Vectorized Processing with Polars
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-11
---

# PY-11 - Vectorized Processing with Polars

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Replace slow Pandas pipelines with high-speed, multi-threaded columnar transformations using Polars.

## Concepts
- **Polars Core Architecture**: Written in Rust atop Apache Arrow memory arrays; utilizes all available CPU cores without Python GIL bottlenecks.
- **DataFrame vs LazyFrame**: Eager execution vs query planning (`lazy()`, optimization graph, `collect()`).
- **The Polars Expression Engine**: Column contexts (`pl.col`), conditional branching (`pl.when().then().otherwise()`), window expressions (`over()`).
- **Memory Efficiency**: Streaming queries (`collect(streaming=True)`) processing larger-than-RAM datasets via chunked processing.

## Learning Resource
- **Title**: Polars Official User Guide
- **Provider / Author**: Polars Development Team
- **URL**: https://docs.pola.rs/
- **Type**: Official Documentation
- **Topic**: Columnar Processing, DataFrames, Lazy Execution
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install Polars: `uv add polars pyarrow`.
- [ ] Load a 5M row CSV lazily via `pl.scan_csv()`.
- [ ] Build a transformation pipeline computing group-by aggregations and 7-day rolling metrics using expressions.
- [ ] Inspect the optimized execution plan using `.explain()` before executing with `.collect()`.

## Completion Criteria
- [ ] Explain why Polars executes significantly faster than Pandas (Rust, Arrow, multi-threading, query optimization).
- [ ] Differentiate between eager `DataFrame` and lazy `LazyFrame` evaluation.
- [ ] Write complex transformations purely using the Polars expression API without Python loops.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Polars | Fast vectorized data processing | Yes (Native) | Yes | `uv add polars` | https://docs.pola.rs/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Polars Expression Example
```python
import polars as pl

lazy_df = (
    pl.scan_csv("orders.csv")
    .filter(pl.col("status") == "COMPLETED")
    .with_columns((pl.col("quantity") * pl.col("unit_price")).alias("total_price"))
    .group_by("customer_id")
    .agg(
        pl.col("total_price").sum().alias("total_spend"),
        pl.len().alias("order_count")
    )
)
print(lazy_df.explain())
result = lazy_df.collect()
```

## Related Lessons
- Prerequisites: [[PY-02 - Strict Type Hinting and mypy]]
- Next Lesson: [[PY-12 - Columnar Serialization with PyArrow]]
- Phase Overview: [[Phase 1 - Foundations]]
