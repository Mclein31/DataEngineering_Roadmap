---
id: OPS-01
title: Docker Fundamentals
phase: Phase 4
module: Module 14: DevOps & Infrastructure as Code
aliases:
  - OPS-01
---

# OPS-01 - Docker Fundamentals

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Master containerization fundamentals: Images, Containers, Namespaces, Cgroups, Layer caching, and Docker CLI commands.

## Concepts
- **Containerization vs Virtualization**: Shared host OS kernel vs heavy guest OS hypervisors. Linux Namespaces (process isolation) and Control Groups / cgroups (resource limits on CPU and RAM).
- **Docker Image Layering**: Read-only stacked filesystem layers; how Docker caches layers to accelerate image builds.
- **Core CLI Operations**: `docker build`, `docker run`, `docker ps`, `docker exec`, `docker logs`, `docker volume`, `docker network`.
- **Port Mapping and Volumes**: Binding container ports to host (`-p 5432:5432`) and mounting persistent host directories (`-v $(pwd)/data:/data`).

## Learning Resource
- **Title**: DataTalksClub Data Engineering Zoomcamp - Module 1: Docker
- **Provider / Author**: Alexey Grigorev et al.
- **URL**: https://github.com/DataTalksClub/data-engineering-zoomcamp
- **Type**: Free Open-Source Course
- **Topic**: Docker, Containers, Port Mapping, Volumes
- **Difficulty**: Intermediate
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Write a `Dockerfile` packaging a Python data ingestion script.
- [ ] Build the image with a tag: `docker build -t de-extractor:v1 .`.
- [ ] Run the container mounting a local directory volume and verify file outputs on the host filesystem.

## Completion Criteria
- [ ] Build and run a custom Docker image packaging Python dependencies.
- [ ] Mount host storage volumes for persistent container data.
- [ ] Explain the difference between container storage and volume mounts.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Docker Desktop / OrbStack | Container engine | Yes (Native) | Yes | `brew install --cask docker` | https://www.docker.com/ |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| LocalStack | Local AWS emulation | Yes | Yes | `docker run localstack/localstack` |

## Notes
### Dockerfile Basics
```dockerfile
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY src/ src/
CMD ["python", "src/extract.py"]
```

## Related Lessons
- Prerequisites: [[LNX-01 - Shell Navigation and Permissions]]
- Next Lesson: [[OPS-02 - Multi-Stage Dockerfiles]]
- Phase Overview: [[Phase 4 - Cloud & DevOps]]
