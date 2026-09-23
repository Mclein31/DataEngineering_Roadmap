---
id: PY-08
title: Context Managers
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-08
---

# PY-08 - Context Managers

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Guarantee clean teardown of database connections, file handles, and temporary cloud resources using context managers.

## Concepts
- **The Context Management Protocol**: The `with` statement, `__enter__()` setup, and `__exit__(exc_type, exc_val, exc_tb)` teardown.
- **Exception Suppression & Propagation**: Returning `True` from `__exit__` to swallow exceptions vs letting errors bubble up.
- **The `contextlib` Standard Module**: `@contextlib.contextmanager` generator-based context managers.
- **Transactional Consistency**: Committing database transactions upon clean exit and rolling back upon unhandled pipeline crashes.

## Learning Resource
- **Title**: Fluent Python (2nd Edition) - Chapter 18: with, match, and else Blocks
- **Provider / Author**: Luciano Ramalho (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/
- **Type**: Textbook
- **Topic**: Context Managers, Resource Safety
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Implement a class-based `DatabaseTransaction` context manager that acquires a connection, commits on success, and executes rollback on error.
- [ ] Implement a generator-based context manager `@contextmanager def ephemeral_scratch_dir()` that creates a temporary directory and recursively deletes it on exit.
- [ ] Test that resource cleanup occurs even when an intentional `ZeroDivisionError` is raised inside the `with` block.

## Completion Criteria
- [ ] Build a custom context manager guaranteeing file handle teardown during abnormal exits.
- [ ] Explain how `__exit__` handles exceptions and when to return `True` vs `False`.
- [ ] Successfully clean up ephemeral scratch storage after pipeline crashes.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Python 3.12+ | Resource management | Yes (Native) | Yes | `Built-in / uv` | https://docs.python.org/3/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Generator Context Manager Pattern
```python
import shutil
import tempfile
from pathlib import Path
from contextlib import contextmanager
from typing import Generator

@contextmanager
def temporary_workspace() -> Generator[Path, None, None]:
    temp_dir = Path(tempfile.mkdtemp())
    try:
        yield temp_dir
    finally:
        shutil.rmtree(temp_dir)
```

## Related Lessons
- Prerequisites: [[PY-06 - Advanced OOP and Protocols]]
- Next Lesson: [[PY-09 - Structured Logging]]
- Phase Overview: [[Phase 1 - Foundations]]
