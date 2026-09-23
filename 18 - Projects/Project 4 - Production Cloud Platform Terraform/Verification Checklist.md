---
id: PRJ-04
name: Verification Checklist - Production Cloud Platform
aliases:
  - PRJ-04 Verification
---

# ✅ PRJ-04 Verification Checklist

- [ ] Terraform code is modularized (`modules/s3`, `modules/iam`, `modules/glue`) and formats cleanly (`terraform fmt -check`).
- [ ] `terraform apply` provisions infrastructure in LocalStack or AWS sandbox without errors.
- [ ] GitHub Actions CI runs Ruff, Pytest, and blocks PR merge upon simulated test failure.
- [ ] Soda Core data quality scan asserts schema contracts and volume bounds post-ingestion.
- [ ] `terraform destroy` cleanly removes all resources without orphaned cloud costs.
