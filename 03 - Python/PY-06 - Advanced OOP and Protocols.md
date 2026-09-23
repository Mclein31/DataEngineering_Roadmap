---
id: PY-06
title: Advanced OOP and Protocols
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-06
---

# PY-06 - Advanced OOP and Protocols

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build modular, pluggable pipeline components and storage connectors using Object-Oriented patterns and static duck typing.

## Concepts
- **Abstract Base Classes (`abc.ABC`, `@abstractmethod`)**: Enforcing nominal interface contracts at runtime.
- **Static Duck Typing with `typing.Protocol` (PEP 544)**: Structural subtyping allowing classes to satisfy interfaces without explicit inheritance.
- **Composition over Inheritance**: Building flexible connectors by composing extractors, transformers, and loaders rather than deep class hierarchies.
- **Dunder Methods for Data Engineering**: `__len__`, `__getitem__`, `__repr__` for custom collections.

## Learning Resource
- **Title**: Fluent Python (2nd Edition) - Chapter 13: Interfaces, Protocols, and ABCs
- **Provider / Author**: Luciano Ramalho (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/
- **Type**: Textbook
- **Topic**: OOP, Protocols, Structural Subtyping
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Define a `DataExtractor(Protocol)` with `extract(self, source_uri: str) -> list[dict[str, Any]]` and `health_check(self) -> bool`.
- [ ] Build `S3Extractor` and `PostgresExtractor` classes that conform to `DataExtractor` without inheriting from a common base class.
- [ ] Write a pipeline runner that accepts any object conforming to `DataExtractor` and verify type compliance with `mypy --strict`.

## Completion Criteria
- [ ] Explain why `typing.Protocol` is superior to rigid subclassing for third-party connector plugins.
- [ ] Verify structural subtyping compliance using `mypy --strict`.
- [ ] Implement a class implementing both `__enter__`/`__exit__` and `Protocol` methods.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| mypy | Protocol validation | Yes (Native) | Yes | `uv add --dev mypy` | https://mypy.readthedocs.io/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Structural Protocol Example
```python
from typing import Protocol, Any

class Extractor(Protocol):
    def extract(self) -> list[dict[str, Any]]: ...
    def ping(self) -> bool: ...

class CustomAPIExtractor:
    def extract(self) -> list[dict[str, Any]]:
        return [{"id": 1, "status": "ok"}]
    def ping(self) -> bool:
        return True

def run_pipeline(ext: Extractor) -> None:
    if ext.ping():
        data = ext.extract()
```

## Related Lessons
- Prerequisites: [[PY-02 - Strict Type Hinting and mypy]]
- Next Lesson: [[PY-07 - Metaprogramming with Decorators]]
- Phase Overview: [[Phase 1 - Foundations]]
