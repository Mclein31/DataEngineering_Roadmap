---
type: project-brain
title: Data Engineering Roadmap — Changelog
project: DataEngineering_Roadmap
last_updated: 2026-09-23
---

# 📜 Data Engineering Roadmap — Changelog

## [1.0.1] - 2026-09-23
### Changed
- **Strict macOS-First Compliance Audit**: Verified that 100% of curriculum lessons, exercises, capstone projects, and setup guides treat macOS (Apple Silicon & Intel) as the primary and supported workstation.
- **Removed OS Switching Friction**: Confirmed zero requirements for Ubuntu, Linux VMs, WSL, or dual-booting.
- **macOS vs Linux Tooling Nuances**: Added explicit macOS BSD vs GNU differences to lessons:
  - `LNX-01`: macOS default Zsh login shell (`~/.zshrc`) vs Bash script execution, and Activity Monitor.
  - `LNX-03`: BSD `sed -i ''` syntax vs GNU `sed -i`, and `brew install gnu-sed` (`gsed`) option.
  - `LNX-04`: Portable `#!/usr/bin/env bash` shebang and Homebrew Bash 5+ guidance.
  - `LNX-05`: macOS Full Disk Access permissions for `/usr/sbin/cron` and `launchd` architectural comparison.
  - `LNX-06`: macOS native `lsof -nP -iTCP:<PORT> -sTCP:LISTEN` standard vs unsupported Linux `netstat -tulpn`.
- **Software Setup Guide**: Added prominent "macOS-First Architecture & Operating Principles" banner to `Software Setup.md`.

## [1.0.0] - 2026-09-23
### Added
- **Full Vault Construction Completed**: Physically constructed all 22 required directories and 186 Markdown documents.
- **Curriculum Architecture**: Authored 137 modular, production-grade lesson files across Modules 02 through 17. Every lesson includes complete YAML frontmatter, objective, deep concepts, curated resources, practice tasks, Definition of Done completion criteria, macOS compatibility tables, notes, and bidirectional wikilinks.
- **Interactive Dashboard**: Built Command Center (`Home.md`), `Daily Log.md`, `Weekly Review.md`, and 40-skill `Skill Matrix.md`.
- **Roadmap & Progression**: Authored Master Roadmap with Mermaid flowcharts, 12-Month execution schedule, Weekly Study System, and Phase 1–5 overview guides.
- **Capstone Projects**: Engineered complete specifications, architecture blueprints, and verification checklists for 5 portfolio projects (Local Modern ELT, Scalable Lakehouse Spark Iceberg, Real-Time Streaming Ingestion, Production Cloud Platform Terraform, Converged Enterprise Lakehouse).
- **Certifications**: Created comprehensive study and preparation tracks for AWS Certified Data Engineer (DEA-C01), Databricks Certified Data Engineer Associate, and Microsoft Fabric Data Engineer (DP-700).
- **Interview Preparation**: Authored 50 High-Frequency SQL Drills, Python Data Wrangling Coding Bank, Systems Internals Question Defense, Behavioral STAR Incident Stories, Portfolio Presentation Playbook, and 30-point Job-Ready Checklist.
- **Resources**: Established central Resource Library (RES-01 to RES-23), macOS Software Setup Guide, Books & PDFs, Official Documentation index, and Practice Platforms directory.
- **Templates**: Standardized Lesson, Project, Weekly, Monthly, and Resource Templates in `99 - Templates/`.
- **Mermaid Diagrams**: Embedded 14 syntactically verified architectural diagrams across the curriculum and capstone projects.
- **Integrity Verification**: Audited vault with 100% passing tests: 0 broken wikilinks across 891 links, 0 placeholders, 100% macOS compatibility.
