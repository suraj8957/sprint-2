# POC – Manual License Scanning using Trivy

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 12-02-2026 | v1.0 | Suraj Tripathi | 12-02-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---

## Repository Scanned

https://github.com/OT-MICROSERVICES/employee-api.git

---

# 📑 Table of Contents

1. [Introduction](#introduction)
2. [Objective](#objective)
3. [Prerequisites](#prerequisites)
4. [Clone Repository](#clone-repository)
5. [Install Trivy](#install-trivy)
6. [Run License Scan](#run-license-scan)
7. [Generate Reports](#generate-reports)
8. [Policy Enforcement](#policy-enforcement)
9. [Scan Validation](#scan-validation)
10. [Best Practices](#best-practices)
11. [Conclusion](#conclusion)
12. [Final Recommendation](#Final-Recommendation)
13. [Contact Information](Contact-Information)

---

## Introduction

This document describes how to manually perform **license scanning** on the `employee-api` repository using **Trivy**.

License scanning helps detect open-source dependency licenses and ensures compliance with internal organizational policies.

---

## Objective

- Scan repository for dependency licenses
- Identify restricted licenses (e.g., GPL)
- Generate compliance report
- Demonstrate manual audit process
- Validate exit codes for CI integration

---

## Prerequisites

- Linux / Ubuntu / WSL
- Git installed
- Trivy installed
- Internet connection

---

## Clone Repository

```bash
git clone https://github.com/OT-MICROSERVICES/employee-api.git
cd employee-api
```

---

## Install Trivy

If not already installed:

```bash
sudo apt-get update
sudo apt-get install -y wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo "deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install -y trivy
```

Verify installation:

```bash
trivy --version
```

---

## Run License Scan

⚠️ Important: In newer Trivy versions, use `--scanners license`

Run scan inside project directory:

```bash
trivy fs --scanners license .
```
<img width="1698" height="465" alt="image" src="https://github.com/user-attachments/assets/de182322-73e6-4645-9191-5396dd29478b" />


This command:

- Scans project dependencies
- Detects license types
- Displays results in table format

---

## Generate Reports

### Table Report

```bash
trivy fs --scanners license -f table -o license-report.txt .
```
<img width="1889" height="582" alt="image" src="https://github.com/user-attachments/assets/0589d568-3a4a-459f-9387-7c1b91775480" />


### JSON Report (Recommended for Audit)

```bash
trivy fs --scanners license -f json -o license-report.json .
```
<img width="1919" height="920" alt="image" src="https://github.com/user-attachments/assets/6c6ea5e0-6e10-4f5e-985f-47d126741ae1" />


This report can be stored for compliance documentation.

---

## Policy Enforcement

To fail build if any license issue is detected:

```bash
trivy fs --scanners license --exit-code 1 .
```

Exit code meaning:

- `0` → No violation
- `1` → License detected (can be used to fail CI)

Check exit code manually:

```bash
echo $?
```

---

## Scan Validation

| Scenario | Expected Result |
|----------|----------------|
| Only MIT/Apache licenses | Scan Pass |
| GPL license detected | Exit Code 1 |
| No dependencies | No issues |
| JSON report generated | File created |

---

## Best Practices

- Perform monthly manual scan
- Store JSON reports with date
- Maintain allowed/blocked license list
- Review new dependencies before release
- Integrate into CI for automation

Example License Policy:

- Allowed: MIT, Apache-2.0, BSD
- Review Required: LGPL, MPL
- Blocked: GPL-3.0

---

## Conclusion

This POC demonstrates successful manual license scanning of the `employee-api` repository using Trivy.

Key Outcomes:

- License detection works properly
- Reports can be generated in multiple formats
- Exit codes enable CI enforcement
- Process is simple and repeatable

### Final Recommendation

Trivy is suitable for manual and CI-based license compliance due to:

- Open-source and free
- Lightweight
- Easy integration
- DevSecOps-friendly
- Supports license + vulnerability scanning

---

## Contact Information
| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) | 

---
