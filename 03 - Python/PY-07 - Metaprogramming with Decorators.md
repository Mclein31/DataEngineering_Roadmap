---
id: PY-07
title: Metaprogramming with Decorators
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-07
---

# PY-07 - Metaprogramming with Decorators

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement cross-cutting pipeline concerns (automated retries, execution timing, rate limiting) using custom Python decorators.

## Concepts
- **Closures & First-Class Functions**: Functions returning inner functions with preserved outer scope state.
- **Decorator Mechanics**: Function syntactic sugar (`@decorator` equivalent to `fn = decorator(fn)`).
- **Preserving Metadata with `functools.wraps`**: Retaining original function name, docstring, and type annotations.
- **Parameterized Decorators**: Writing three-level nested closures to accept configuration arguments (e.g., `@retry(max_attempts=3)`).

## Learning Resource
- **Title**: Fluent Python (2nd Edition) - Chapter 9: Decorators and Closures
- **Provider / Author**: Luciano Ramalho (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/
- **Type**: Textbook
- **Topic**: Decorators, Closures, Metaprogramming
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Implement a `@timer` decorator that calculates and logs execution duration in milliseconds.
- [ ] Implement a `@retry(max_attempts=3, backoff_seconds=1.0)` decorator that catches network exceptions and retries with backoff.
- [ ] Decorate an unstable API client function and verify retry behavior under simulated network drops.

## Completion Criteria
- [ ] Implement a custom parameterized `@retry` decorator using `functools.wraps`.
- [ ] Preserve function signatures so `mypy --strict` passes with type annotations.
- [ ] Log execution timing and call metadata across decorated ETL functions.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Python 3.12+ | Decorator runtime | Yes (Native) | Yes | `Built-in / uv` | https://docs.python.org/3/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Parameterized Retry Decorator
```python
import time
from functools import wraps
from typing import Callable, TypeVar, Any

F = TypeVar("F", bound=Callable[..., Any])

def retry(max_attempts: int = 3, delay: float = 1.0) -> Callable[[F], F]:
    def decorator(func: F) -> F:
        @wraps(func)
        def wrapper(*args: Any, **kwargs: Any) -> Any:
            for attempt in range(1, max_attempts + 1):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt == max_attempts:
                        raise
                    time.sleep(delay * attempt)
        return wrapper  # type: ignore[return-value]
    return decorator
```

## Related Lessons
- Prerequisites: [[PY-06 - Advanced OOP and Protocols]]
- Next Lesson: [[PY-08 - Context Managers]]
- Phase Overview: [[Phase 1 - Foundations]]
