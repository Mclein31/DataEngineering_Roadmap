---
id: PY-13
title: Unit Testing with pytest
phase: Phase 1
module: Module 03: Production Python & Software Engineering
aliases:
  - PY-13
---

# PY-13 - Unit Testing with pytest

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build automated, deterministic unit and integration test suites for pipeline components using pytest fixtures and mocks.

## Concepts
- **The `pytest` Testing Framework**: Test discovery conventions (`test_*.py`), standard `assert` evaluation without boilerplate.
- **Fixtures (`@pytest.fixture`)**: Reusable test setups, scoping (`function`, `module`, `session`), and teardown via `yield`.
- **Parametrized Testing (`@pytest.mark.parametrize`)**: Testing multiple edge cases and boundary inputs across a single test function.
- **Mocking External Dependencies**: Using `monkeypatch` and `unittest.mock` to mock database connections and REST API calls.

## Learning Resource
- **Title**: pytest Official Documentation
- **Provider / Author**: pytest Development Team
- **URL**: https://docs.pytest.org/en/stable/
- **Type**: Official Documentation
- **Topic**: Automated Unit Testing, Fixtures, Mocking
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Add pytest and pytest-cov: `uv add --dev pytest pytest-cov`.
- [ ] Write unit tests for a data cleansing module testing null inputs, negative amounts, and invalid dates.
- [ ] Write a parametrized test testing 5 different invalid email address formats.
- [ ] Execute test suite and verify coverage: `uv run pytest --cov=src tests/`.

## Completion Criteria
- [ ] Achieve >= 85% test coverage on a Python ingestion module using `pytest-cov`.
- [ ] Mock an external HTTP API response in a unit test without making live network requests.
- [ ] Write a reusable fixture creating ephemeral sample Parquet data for integration testing.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| pytest | Automated test runner | Yes (Native) | Yes | `uv add --dev pytest pytest-cov` | https://docs.pytest.org/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | IDE for Python/SQL development | Yes | Yes | Free editor with Python extensions |

## Notes
### Parametrized Test Example
```python
import pytest
from src.validator import is_valid_transaction_id

@pytest.mark.parametrize("txn_id,expected", [
    ("TXN-12345", True),
    ("txn-12345", False),
    ("", False),
    ("INVALID-99", False),
])
def test_transaction_id_validation(txn_id: str, expected: bool) -> None:
    assert is_valid_transaction_id(txn_id) == expected
```

## Related Lessons
- Prerequisites: [[PY-03 - Data Validation with Pydantic]], [[PY-06 - Advanced OOP and Protocols]]
- Next Lesson: [[PY-14 - Python Packaging with pyproject]]
- Phase Overview: [[Phase 1 - Foundations]]
