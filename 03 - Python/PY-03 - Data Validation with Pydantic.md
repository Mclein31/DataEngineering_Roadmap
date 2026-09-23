---
id: PY-03
title: Data Validation with Pydantic
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-03
---

# PY-03 - Data Validation with Pydantic

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Enforce strict schema boundaries on incoming dirty data from APIs, files, and databases using Pydantic v2.

## Concepts
- **Pydantic v2 Core Architecture**: Powered by `pydantic-core` in Rust, parsing and validating JSON/dicts 5–20x faster than Pydantic v1.
- **Model Definition**: `BaseModel`, `Field` constraints (`gt=0`, `max_length=50`), custom field types (`EmailStr`, `HttpUrl`).
- **Validators**: `@field_validator` (sanitizing and coercing single fields) and `@model_validator(mode='after')` (cross-field validation).
- **Graceful Error Handling**: Catching `ValidationError` and serializing error details to route corrupt records to a Dead Letter Queue (DLQ).

## Learning Resource
- **Title**: Pydantic v2 Official Documentation
- **Provider / Author**: Pydantic Services Inc.
- **URL**: https://docs.pydantic.dev/latest/
- **Type**: Official Documentation
- **Topic**: Data Validation, Parsing, Schemas
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Define an `OrderSchema` model with `order_id` (str), `customer_id` (int), `amount` (float > 0), and `order_date` (datetime).
- [ ] Add a `@field_validator` that strips whitespace and validates email formatting.
- [ ] Write a parsing function that ingests a list of dirty JSON records, instantiates models, and routes malformed records to a separate DLQ list with validation error logs.

## Completion Criteria
- [ ] Write a custom Pydantic validator that normalizes incoming data and rejects negative financial values.
- [ ] Handle `ValidationError` gracefully by extracting failed field names and messages into machine-readable logs.
- [ ] Export validated Pydantic models to JSON and dicts using `model_dump()` and `model_dump_json()`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Pydantic v2 | Data validation and parsing | Yes (Native) | Yes | `uv add pydantic` | https://docs.pydantic.dev/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Pydantic v2 Pattern
```python
from datetime import datetime
from pydantic import BaseModel, Field, field_validator

class Transaction(BaseModel):
    txn_id: str
    amount: float = Field(gt=0, description="Amount must be positive")
    timestamp: datetime
    
    @field_validator("txn_id")
    @classmethod
    def validate_txn_id(cls, v: str) -> str:
        v = v.strip().upper()
        if not v.startswith("TXN-"):
            raise ValueError("Transaction ID must begin with 'TXN-'")
        return v
```

## Related Lessons
- Prerequisites: [[PY-02 - Strict Type Hinting and mypy]]
- Next Lesson: [[PY-04 - Functional Mechanics and Itertools]]
- Phase Overview: [[Phase 1 - Foundations]]
