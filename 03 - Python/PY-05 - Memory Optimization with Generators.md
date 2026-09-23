---
id: PY-05
title: Memory Optimization with Generators
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-05
---

# PY-05 - Memory Optimization with Generators

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Stream multi-gigabyte files and database cursors with near-zero RAM footprint using custom Python generators.

## Concepts
- **The Python Iterator Protocol**: `__iter__()` returning the iterator and `__next__()` raising `StopIteration`.
- **The `yield` Keyword**: Suspending function execution state, preserving local variables, and resuming upon the next iteration.
- **Generator Expressions vs List Comprehensions**: `(x for x in data)` (lazy `generator` object) vs `[x for x in data]` (eager `list` allocation).
- **Profiling Memory Footprint**: Measuring memory usage with `sys.getsizeof()` and tracking peak RSS with `tracemalloc`.

## Learning Resource
- **Title**: Fluent Python (2nd Edition) - Chapter 17: Iterators, Generators, and Classic Coroutines
- **Provider / Author**: Luciano Ramalho (O'Reilly)
- **URL**: https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/
- **Type**: Textbook
- **Topic**: Generators, Iterators, Memory Optimization
- **Difficulty**: Advanced
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write a script generating a synthetic 2GB CSV file with 10 million rows.
- [ ] Implement a generator function `stream_rows(file_path)` that opens the file and yields parsed, stripped line dictionaries.
- [ ] Profile memory usage using `tracemalloc` while iterating through the entire 2GB file, proving peak RAM stays below 30MB.

## Completion Criteria
- [ ] Process a 2GB file in Python while keeping RAM utilization strictly below 50MB.
- [ ] Articulate the internal state preservation of a generator function when paused at a `yield` statement.
- [ ] Implement a generator pipeline chaining 3 generator functions (extract -> filter -> transform).

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Python 3.12+ | Generator runtimes | Yes (Native) | Yes | `Built-in / uv` | https://docs.python.org/3/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Generator Streaming Pipeline
```python
from typing import Generator
import tracemalloc

def read_lines(filepath: str) -> Generator[str, None, None]:
    with open(filepath, "r", encoding="utf-8") as f:
        for line in f:
            yield line.strip()

def parse_csv(lines: Generator[str, None, None]) -> Generator[list[str], None, None]:
    for line in lines:
        yield line.split(",")

tracemalloc.start()
for row in parse_csv(read_lines("large_dataset.csv")):
    pass
current, peak = tracemalloc.get_traced_memory()
print(f"Peak memory: {peak / 1024 / 1024:.2f} MB")
tracemalloc.stop()
```

## Related Lessons
- Prerequisites: [[PY-04 - Functional Mechanics and Itertools]]
- Next Lesson: [[PY-06 - Advanced OOP and Protocols]]
- Phase Overview: [[Phase 1 - Foundations]]
