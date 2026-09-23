---
title: Software Setup & Installation Guide
aliases:
  - Software Setup
---

# 💻 macOS Software Setup & Installation Guide

This guide details all tools utilized throughout the Data Engineering roadmap. Every tool is **100% compatible with macOS (Apple Silicon M1/M2/M3/M4 & Intel)**, and every core requirement is **free and open-source**.

---

## 🍎 macOS-First Architecture & Operating Principles

This roadmap treats **macOS as your primary and fully supported workstation**. You do **NOT** need to install Ubuntu, dual-boot, maintain a Linux VM, use WSL, or switch operating systems at any point in this curriculum.

### Core macOS Advantages for Data Engineers
1. **Certified Unix Foundation**: macOS is built on a certified BSD Unix foundation (`Darwin`). Core data tools (`ssh`, `curl`, `awk`, `sed`, `grep`, `zsh`, `chmod`, `lsof`) run natively in macOS Terminal with zero virtualization.
2. **Native Runtimes**: Modern analytical runtimes like **DuckDB**, **Polars**, **Apache Spark (PySpark)**, **dbt-core**, and **uv (Python 3.12+)** compile directly to native ARM64 (Apple Silicon) and x86_64 binaries with maximum performance.
3. **Containerized Linux without VM Overhead**: When a distributed service requires a container environment (such as multi-broker **Apache Kafka KRaft**, **PostgreSQL 16**, or **LocalStack AWS emulation**), you run them seamlessly through **Docker Desktop for Mac** or **OrbStack**. You never need to manage a separate Linux operating system.

### Operating Rules
- **Terminal**: Use macOS native Terminal or iTerm2 with `zsh`.
- **Package Management**: Install all native packages via **Homebrew** (`brew`).
- **Python**: Use **uv** (`brew install uv`) for virtual environment isolation and package resolution.
- **No Paid Software**: All required tools are 100% free and open-source or free personal tier.

---

## 🛠️ Category 1: Essential Tools (Foundational)

### 1. Homebrew
- **Purpose**: macOS package manager for installing command-line utilities, compilers, and runtimes.
- **macOS Compatible**: Yes (Native Apple Silicon & Intel)
- **Free**: Yes (Open Source)
- **Official Website**: https://brew.sh/
- **Installation Method**:
  ```bash
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  ```
- **When I Need It**: Month 1 (Pre-course setup)
- **Free Alternative**: Self-contained binaries.

### 2. uv (Fast Python Package Manager)
- **Purpose**: Ultra-fast Python package resolver, virtual environment manager, and Python version installer.
- **macOS Compatible**: Yes (Native)
- **Free**: Yes (Open Source)
- **Official Website**: https://docs.astral.sh/uv/
- **Installation Method**:
  ```bash
  brew install uv
  # Or via official curl installer:
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- **When I Need It**: Month 1 (Lesson [[PY-01 - Python Internals and uv|PY-01]])
- **Disk Impact**: ~40MB
- **Free Alternative**: Standard `venv` / `pip` (orders of magnitude slower).

### 3. Docker Desktop / OrbStack
- **Purpose**: Container engine for running isolated databases (Postgres), message brokers (Kafka), and local cloud emulators (LocalStack, MinIO).
- **macOS Compatible**: Yes (Native Apple Silicon ARM64 & Intel x86_64)
- **Free**: Yes (Docker Desktop free for personal use; OrbStack has a generous free tier)
- **Official Website**: https://www.docker.com/products/docker-desktop/ (OrbStack: https://orbstack.dev/)
- **Installation Method**:
  ```bash
  brew install --cask docker
  # Or for a lightweight alternative:
  brew install --cask orbstack
  ```
- **When I Need It**: Month 1 (Lesson [[SQL-01 - Relational Execution Order|SQL-01]] / [[DB-01 - Row vs Columnar Storage|DB-01]])
- **Disk Impact**: ~2–4GB

### 4. PostgreSQL 16 (via Docker)
- **Purpose**: Relational OLTP database engine for SQL practice, transaction benchmarking, and source data.
- **macOS Compatible**: Yes (via Docker)
- **Free**: Yes (Open Source)
- **Official Website**: https://www.postgresql.org/
- **Installation Method**:
  ```bash
  docker run --name de-postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:16
  ```
- **When I Need It**: Month 1 (Lesson [[SQL-01 - Relational Execution Order|SQL-01]])
- **Free Alternative**: `brew install postgresql@16` (Docker preferred for environment isolation).

### 5. DuckDB
- **Purpose**: High-performance in-process columnar analytical query engine.
- **macOS Compatible**: Yes (Native CLI & Python library)
- **Free**: Yes (Open Source)
- **Official Website**: https://duckdb.org/
- **Installation Method**:
  ```bash
  brew install duckdb
  # In your uv environment:
  uv pip install duckdb
  ```
- **When I Need It**: Month 3 (Lesson [[DBT-02 - Embedded Analytics with DuckDB|DBT-02]])
- **Disk Impact**: ~30MB

### 6. dbt-core
- **Purpose**: In-warehouse transformation, data modeling, testing, and documentation framework.
- **macOS Compatible**: Yes (via Python)
- **Free**: Yes (Open Source)
- **Official Website**: https://docs.getdbt.com/
- **Installation Method**:
  ```bash
  uv pip install dbt-core dbt-duckdb dbt-postgres
  ```
- **When I Need It**: Month 5 (Lesson [[DBT-03 - dbt Core Setup and Architecture|DBT-03]])

---

## ⚙️ Category 2: Scale, Distributed & Streaming Tools

### 7. Apache Spark 4.0 (PySpark)
- **Purpose**: Distributed compute engine for large-scale data manipulation and Spark Structured Streaming.
- **macOS Compatible**: Yes (via Python PySpark Connect)
- **Free**: Yes (Open Source)
- **Official Website**: https://spark.apache.org/
- **Installation Method**:
  ```bash
  uv pip install pyspark==4.0.0
  ```
- **When I Need It**: Month 7 (Lesson [[SPK-01 - Spark 4 Cluster Architecture|SPK-01]])
- **Disk Impact**: ~350MB

### 8. Apache Kafka 4.0 (KRaft Mode via Docker)
- **Purpose**: High-throughput distributed event streaming platform running without ZooKeeper.
- **macOS Compatible**: Yes (via Docker)
- **Free**: Yes (Open Source Apache 2.0)
- **Official Website**: https://kafka.apache.org/
- **Installation Method**: Deployed via Docker Compose service (provided in [[KFK-02 - Kafka 4 KRaft Consensus|KFK-02]]).
- **When I Need It**: Month 8 (Lesson [[KFK-01 - Event-Driven Fundamentals|KFK-01]])

### 9. Apache Airflow 3.x
- **Purpose**: Programmatic workflow orchestration with TaskFlow API and event-driven `@asset` scheduling.
- **macOS Compatible**: Yes (Docker Compose or uv venv)
- **Free**: Yes (Open Source)
- **Official Website**: https://airflow.apache.org/
- **Installation Method**: Official Docker Compose configuration.
- **When I Need It**: Month 8 (Lesson [[AIR-01 - Orchestration Principles|AIR-01]])

---

## ☁️ Category 3: Cloud, IaC & DevOps Tools

### 10. Terraform
- **Purpose**: Declarative Infrastructure as Code (IaC) tool for provisioning cloud and local resources.
- **macOS Compatible**: Yes (Native binary)
- **Free**: Yes (Open Source MPL-2.0 / BSL)
- **Official Website**: https://developer.hashicorp.com/terraform
- **Installation Method**:
  ```bash
  brew tap hashicorp/tap
  brew install hashicorp/tap/terraform
  ```
- **When I Need It**: Month 9 (Lesson [[OPS-04 - Terraform Syntax and State|OPS-04]])

### 11. LocalStack (Local AWS Cloud Emulator)
- **Purpose**: Fully functional local AWS cloud emulation in Docker (eliminates accidental AWS billing).
- **macOS Compatible**: Yes (via Docker)
- **Free**: Yes (Community Edition 100% Free)
- **Official Website**: https://localstack.cloud/
- **Installation Method**:
  ```bash
  docker run --rm -d --name localstack -p 4566:4566 -p 4510-4559:4510-4559 localstack/localstack
  ```
- **When I Need It**: Month 9 (Lesson [[CLD-01 - AWS IAM Security|CLD-01]])
- **Billing Risk**: Zero (100% local)

### 12. AWS CLI
- **Purpose**: Command-line interface for interacting with AWS services and LocalStack.
- **macOS Compatible**: Yes (Native)
- **Free**: Yes
- **Official Website**: https://aws.amazon.com/cli/
- **Installation Method**:
  ```bash
  brew install awscli
  ```
- **When I Need It**: Month 9 (Lesson [[CLD-01 - AWS IAM Security|CLD-01]])

---

## ⚠️ Cloud Cost Governance Warning

> [!WARNING] Cloud Billing Guardrails
> While AWS Free Tier offers 12 months of introductory services (e.g., 5GB S3, 1M Glue requests), running resources such as EMR clusters, RDS databases, or unpartitioned Athena queries can generate unexpected charges.
>
> **Rules for Cloud Exercises**:
> 1. Complete all exercises in **LocalStack** or local containers first.
> 2. When using a live AWS account, configure an **AWS Billing Alarm** at $5.00 USD immediately.
> 3. Always run `terraform destroy` immediately upon completing an exercise.
