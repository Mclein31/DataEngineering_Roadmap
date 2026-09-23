---
id: LNX-06
title: Networking Fundamentals for DE
phase: Phase 1
module: Module 02: Systems Foundations, Linux & Git
aliases:
  - LNX-06
---

# LNX-06 - Networking Fundamentals for DE

## Status
- [ ] Not Started
- [ ] In Progress
- [ ] Completed

## Objective
Diagnose connectivity issues between local pipelines, database ports, Docker networks, and remote APIs.

## Concepts
- **TCP/IP & Port Binding**: Port binding, loopback (`127.0.0.1`), standard ports (Postgres 5432, Kafka 9092).
- **Socket & Port Inspection**: `lsof -i :<port>` to resolve port conflicts.
- **HTTP Protocol Mechanics**: Verbs, headers, response status codes (401, 403, 429, 502, 503).
- **SSH & Key Management**: `ssh-keygen -t ed25519` and `~/.ssh/config`.

## Learning Resource
- **Title**: Linux Journey (Networking Fundamentals)
- **Provider / Author**: Linux Journey Community
- **URL**: https://linuxjourney.com/
- **Type**: Interactive Tutorial
- **Topic**: Networking, Ports, SSH, curl
- **Difficulty**: Beginner
- **Category**: 🔥 ESSENTIAL

## Practice
- [ ] Use `lsof -i :5432` to inspect if any process is occupying the default PostgreSQL port.
- [ ] Inspect HTTP response headers of an external API using `curl -I -s https://httpbin.org/status/429`.
- [ ] Generate an SSH keypair using `ssh-keygen -t ed25519`.

## Completion Criteria
- [ ] Explain the difference between HTTP status codes 401, 403, 429, and 502.
- [ ] Identify and kill a process blocking a required database port.
- [ ] Generate an Ed25519 SSH keypair.

## Software / Tools

### Required Software
| Tool | Purpose | macOS Compatible | Free | Installation Method | Official Resource |
| :--- | :--- | :--- | :--- | :--- | :--- |
| curl, lsof, ssh (macOS) | Network diagnostics | Yes (Native) | Yes | `Built-in` | https://support.apple.com/terminal |

### Optional Software
| Tool | Purpose | macOS Compatible | Free | Purpose / Note |
| :--- | :--- | :--- | :--- | :--- |
| VS Code | Script editing | Yes | Yes | Free editor |

## Notes
### Port Diagnostics
```bash
# Inspect process listening on PostgreSQL port (macOS native):
lsof -nP -iTCP:5432 -sTCP:LISTEN

# Check external HTTP status code:
curl -I -s https://httpbin.org/status/200
```

### 🍎 macOS vs Linux Network Inspection
On Linux servers, developers often run `netstat -tulpn` or `ss -tulpn`. These flags are **not supported** on macOS BSD `netstat`.
On macOS, the native, high-precision standard for port inspection and process resolution is `lsof`:
```bash
# macOS: List listening sockets with numeric ports and PID:
lsof -nP -iTCP:<PORT> -sTCP:LISTEN

# Gracefully terminate conflicting database or broker process:
kill -15 <PID>
```

## Related Lessons
- Prerequisites: [[LNX-01 - Shell Navigation and Permissions]]
- Next Lesson: [[GIT-01 - Git Internals and Staging]]
- Phase Overview: [[Phase 1 - Foundations]]
