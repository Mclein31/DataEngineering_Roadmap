---
id: PY-09
title: Structured Logging
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-09
---

# PY-09 - Structured Logging

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Implement machine-readable, traceable structured JSON logging across pipeline execution boundaries.

## Concepts
- **Structured vs Unstructured Logging**: Why `print()` and arbitrary string interpolation fail in production log aggregators (Datadog, CloudWatch).
- **JSON Formatting**: Emitting key-value event logs (`timestamp`, `level`, `pipeline_id`, `record_count`, `duration_ms`).
- **Context Binding (`structlog`)**: Binding persistent execution metadata (run ID, environment, partition date) across child log calls.
- **Exception Chaining**: Preserving original tracebacks using `raise ... from ...` and serializing stack traces in error logs.

## Learning Resource
- **Title**: Python Official Logging Tutorial & structlog Docs
- **Provider / Author**: Python Software Foundation / structlog
- **URL**: https://docs.python.org/3/howto/logging.html
- **Type**: Official Documentation
- **Topic**: Structured Logging, Observability
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Add `structlog` to your project: `uv add structlog`.
- [ ] Configure `structlog` to emit JSON-formatted logs with ISO timestamps, log levels, and contextual metadata.
- [ ] Replace all `print()` statements in an extraction module with level-appropriate structured logs (`logger.info`, `logger.error`).

## Completion Criteria
- [ ] Replace unstructured print statements with machine-readable JSON logs.
- [ ] Bind execution context (e.g., `execution_id`) across all log messages within a pipeline run.
- [ ] Serialize exception stack traces cleanly into log payloads.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| structlog | Structured JSON logging | Yes (Native) | Yes | `uv add structlog` | https://www.structlog.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### structlog Setup
```python
import structlog

structlog.configure(
    processors=[
        structlog.processors.TimeStamper(fmt="iso"),
        structlog.processors.add_log_level,
        structlog.processors.JSONRenderer()
    ]
)
logger = structlog.get_logger()
log = logger.bind(pipeline_run_id="run-8492")
log.info("Batch processed", records_ingested=5000, duration_seconds=1.24)
```

## Related Lessons
- Prerequisites: [[PY-01 - Python Internals and uv]]
- Next Lesson: [[PY-10 - Resilient HTTP Ingestion with httpx]]
- Phase Overview: [[Phase 1 - Foundations]]
