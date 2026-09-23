---
id: DAT-03
title: Validation with Great Expectations
phase: Phase 4
module: Module 15: Data Reliability Engineering & Observability
aliases:
  - DAT-03
---

# DAT-03 - Validation with Great Expectations

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build automated data validation suites and render interactive Data Docs using Great Expectations (GX).

## Concepts
- **Great Expectations Framework**: Enterprise Python validation framework built around Expectation Suites, Data Contexts, and Checkpoints.
- **Core Expectations**:
  - `expect_column_values_to_not_be_null`
  - `expect_column_values_to_be_between`
  - `expect_column_values_to_match_regex`
  - `expect_table_row_count_to_be_between`
- **Data Docs**: Auto-generated interactive HTML reports rendering test results, schema definitions, and visual distribution graphs.
- **GX vs Soda Core**: Great Expectations (deep Python programmatic control, heavy setup) vs Soda Core (lightweight YAML-first syntax, faster setup).

## Learning Resource
- **Title**: Great Expectations Official Documentation
- **Provider / Author**: Great Expectations
- **URL**: https://docs.greatexpectations.io/docs/
- **Type**: Official Documentation
- **Topic**: Great Expectations, Validation Suites, Data Docs
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Install Great Expectations: `uv pip install great_expectations`.
- [ ] Create an Expectation Suite for an extracted customer dataframe in Python.
- [ ] Validate the batch and generate local interactive Data Docs HTML reports.

## Completion Criteria
- [ ] Build an Expectation Suite containing at least 4 distinct data assertions.
- [ ] Generate and view visual Data Docs HTML reports locally.
- [ ] Compare architectural trade-offs between Great Expectations and Soda Core.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Great Expectations | Data validation framework | Yes | Yes | `uv pip install great_expectations` | https://greatexpectations.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Great Expectations Code Pattern
```python
import great_expectations as gx

context = gx.get_context()
validator = context.sources.pandas_default.read_csv("orders.csv")
validator.expect_column_values_to_not_be_null(column="order_id")
validator.expect_column_values_to_be_between(column="amount", min_value=0.01)
checkpoint_result = validator.validate()
```

## Related Lessons
- Prerequisites: [[DAT-02 - Pipeline Testing with Soda Core]]
- Next Lesson: [[DAT-04 - Data Contracts]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
