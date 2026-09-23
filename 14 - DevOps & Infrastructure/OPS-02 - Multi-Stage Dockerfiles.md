---
id: OPS-02
title: Multi-Stage Dockerfiles
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-02
---

# OPS-02 - Multi-Stage Dockerfiles

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Build secure, lightweight multi-stage Dockerfiles that eliminate compilers, reduce image sizes by > 80%, and enforce non-root security.

## Concepts
- **The Bloated Container Hazard**: Compilers (`gcc`, `g++`), build caches, and test suites left inside production containers create 1GB+ images and massive CVE security vulnerabilities.
- **Multi-Stage Builds (`FROM ... AS builder`)**:
  - *Stage 1 (Builder)*: Installs compilers, packages wheels via `uv`, compiles dependencies.
  - *Stage 2 (Runtime)*: Minimal slim base image; copies only compiled wheels and application code from builder stage.
- **Security Hardening**: Creating and running as a non-root user (`USER appuser`) to prevent privilege escalation attacks.

## Learning Resource
- **Title**: Docker Official Documentation - Multi-stage builds
- **Provider / Author**: Docker Inc.
- **URL**: https://docs.docker.com/build/building/multi-stage/
- **Type**: Official Documentation
- **Topic**: Multi-Stage Dockerfiles, Optimization, Security
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write a single-stage Dockerfile packaging a Polars and PyArrow pipeline; observe resulting image size (~850MB).
- [ ] Refactor into a multi-stage Dockerfile using `python:3.12-slim` and `uv`; measure final image size (<150MB).
- [ ] Configure `USER appuser` and verify the container refuses root access.

## Completion Criteria
- [ ] Reduce Docker image footprint by > 75% using multi-stage builds.
- [ ] Eliminate build tools (`gcc`, build-essential) from final runtime image.
- [ ] Run container processes under a non-root UID.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker Desktop | Image compilation | Yes | Yes | `brew install --cask docker` | https://www.docker.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Production Multi-Stage Dockerfile
```dockerfile
# Stage 1: Build stage
FROM python:3.12-slim AS builder
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/uv
WORKDIR /app
COPY pyproject.toml uv.lock ./
RUN uv sync --frozen --no-dev --no-install-project

# Stage 2: Minimal Runtime stage
FROM python:3.12-slim
WORKDIR /app
RUN addgroup --system appgroup && adduser --system --group appuser
COPY --from=builder /app/.venv /app/.venv
COPY src/ src/
ENV PATH="/app/.venv/bin:$PATH"
USER appuser
CMD ["python", "src/main.py"]
```

## Related Lessons
- Prerequisites: [[OPS-01 - Docker Fundamentals]]
- Next Lesson: [[OPS-03 - Docker Compose Platforms]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
