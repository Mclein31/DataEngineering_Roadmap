---
id: PY-02
title: Strict Type Hinting and mypy
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-02
---

# PY-02 - Strict Type Hinting and mypy

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Eliminate runtime type bugs and silent pipeline failures using static type enforcement with mypy in strict mode.

## Concepts
- **Python Type System (PEP 484/585/604)**: Built-in generics (`list[str]`, `dict[str, Any]`, `set[int]`), union syntax (`str | None`), `Callable`, `TypeVar`.
- **Static Analysis vs Runtime Overhead**: Type hints exist purely for static analysis tools; they have zero runtime execution performance cost.
- **The Danger of `Any`**: How unchecked `Any` propagates silently through pipeline code, defeating type safety.
- **Enforcing `mypy --strict`**: Requiring explicit return types, disallowing untyped definitions, and flagging unhandled `None` values.

## Learning Resource
- **Title**: Python 3.12+ Typing Documentation
- **Provider / Author**: Python Software Foundation
- **URL**: https://docs.python.org/3/library/typing.html
- **Type**: Official Documentation
- **Topic**: Static Type Hinting, mypy
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Add mypy to your project: `uv add --dev mypy`.
- [ ] Write a 100-line data ingestion script with comprehensive type annotations across all function parameters and returns.
- [ ] Run `uv run mypy --strict .` and systematically resolve all detected typing violations.

## Completion Criteria
- [ ] Run `mypy --strict` on a multi-function data extraction module with zero errors.
- [ ] Correctly handle nullable inputs using `str | None` with explicit guard assertions.
- [ ] Explain the runtime performance implications of static typing in Python (none).

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| mypy | Static type checker | Yes (Native) | Yes | `uv add --dev mypy` | https://mypy.readthedocs.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Typing Example
```python
from typing import Any
from collections.abc import Callable

def parse_record(raw: dict[str, Any], validator: Callable[[dict[str, Any]], bool]) -> dict[str, str | int] | None:
    if not validator(raw):
        return None
    return {"id": int(raw["id"]), "name": str(raw["name"])}
```

## Related Lessons
- Prerequisites: [[PY-01 - Python Internals and uv]]
- Next Lesson: [[PY-03 - Data Validation with Pydantic]]
- Phase Overview: [[Phase 1 - Foundations]]
