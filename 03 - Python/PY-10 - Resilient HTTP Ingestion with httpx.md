---
id: PY-10
title: Resilient HTTP Ingestion with httpx
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-10
---

# PY-10 - Resilient HTTP Ingestion with httpx

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Ingest remote REST API datasets handling pagination, rate limiting (`HTTP 429`), timeouts, and exponential backoff.

## Concepts
- **Modern HTTP with `httpx`**: Synchronous and asynchronous clients, HTTP/2 support, connection pooling.
- **Handling Pagination Strategies**: Offset/limit pagination, page numbers, and cursor/token-based pagination.
- **Rate Limit Headers**: Parsing `Retry-After`, `X-RateLimit-Remaining`, and `X-RateLimit-Reset`.
- **Jittered Exponential Backoff**: Adding randomized intervals to backoff algorithms to prevent the "thundering herd" problem.

## Learning Resource
- **Title**: HTTPX Official Documentation
- **Provider / Author**: Encode OSS
- **URL**: https://www.python-httpx.org/
- **Type**: Official Documentation
- **Topic**: HTTP Client, API Ingestion
- **Difficulty**: Intermediate
- **Category**: ⭐ RECOMMENDED

## Practice
- [ ] Add `httpx` to your environment: `uv add httpx`.
- [ ] Build an API extractor fetching paginated user records from an open REST API (e.g., GitHub public API or JSONPlaceholder).
- [ ] Implement a token-bucket or exponential sleep algorithm when `HTTP 429` status is received.

## Completion Criteria
- [ ] Ingest 50 pages of paginated API data without missing records or looping infinitely.
- [ ] Implement exponential backoff with jitter on network dropouts.
- [ ] Use `httpx.Client()` context manager to pool connections efficiently.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| httpx | HTTP client library | Yes (Native) | Yes | `uv add httpx` | https://www.python-httpx.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Paginated Extractor Pattern
```python
import httpx

def fetch_all_pages(base_url: str) -> list[dict]:
    all_data = []
    page = 1
    with httpx.Client(timeout=10.0) as client:
        while True:
            resp = client.get(f"{base_url}?page={page}&limit=100")
            resp.raise_for_status()
            items = resp.json()
            if not items:
                break
            all_data.extend(items)
            page += 1
    return all_data
```

## Related Lessons
- Prerequisites: [[PY-03 - Data Validation with Pydantic]], [[PY-07 - Metaprogramming with Decorators]]
- Next Lesson: [[PY-11 - Vectorized Processing with Polars]]
- Phase Overview: [[Phase 1 - Foundations]]
