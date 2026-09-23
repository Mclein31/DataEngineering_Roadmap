---
id: OPS-03
title: Docker Compose Platforms
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-03
---

# OPS-03 - Docker Compose Platforms

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Orchestrate multi-container local data platforms (Postgres, MinIO, Kafka, Metabase) with shared networks and healthchecks.

## Concepts
- **Multi-Service Coordination**: Defining entire local data architectures in a single declarative `docker-compose.yml` file.
- **Service Networking**: Automatic internal DNS resolution (services communicate by container name, e.g. `http://kafka:9092` or `postgres:5432`).
- **Healthchecks & Dependencies (`depends_on: condition: service_healthy`)**: Preventing dependent pipeline containers from crashing before databases finish initializing.
- **Environment & Volume Management**: Centralizing `.env` files and persistent named volumes.

## Learning Resource
- **Title**: Docker Compose Official Documentation
- **Provider / Author**: Docker Inc.
- **URL**: https://docs.docker.com/compose/
- **Type**: Official Documentation
- **Topic**: Docker Compose, Networking, Service Orchestration
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Create a `docker-compose.yml` defining PostgreSQL 16, Adminer GUI, and MinIO object storage.
- [ ] Configure explicit healthchecks verifying Postgres responds to `pg_isready` before downstream services start.
- [ ] Launch the entire multi-service stack with a single command: `docker compose up -d`.

## Completion Criteria
- [ ] Orchestrate at least 3 coordinated services via Docker Compose.
- [ ] Configure container healthchecks and startup order with `condition: service_healthy`.
- [ ] Tear down the environment cleanly with `docker compose down -v`.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker Compose | Multi-container platforms | Yes | Yes | `Built-in with Docker` | https://docs.docker.com/compose/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Docker Compose with Healthchecks
```yaml
version: '3.8'
services:
  postgres:
    image: postgres:16
    environment:
      POSTGRES_PASSWORD: secretpassword
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U postgres"]
      interval: 5s
      timeout: 5s
      retries: 5

  pipeline:
    build: .
    depends_on:
      postgres:
        condition: service_healthy
```

## Related Lessons
- Prerequisites: [[OPS-02 - Multi-Stage Dockerfiles]]
- Next Lesson: [[OPS-04 - Terraform Syntax and State]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
