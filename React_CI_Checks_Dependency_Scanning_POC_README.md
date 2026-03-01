# React Dependency Scanning – POC
---
---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---
## 1. Introduction

Modern React applications depend heavily on third-party npm packages. While these dependencies improve development speed, they may introduce security vulnerabilities and license compliance risks.

This document demonstrates how to perform dependency scanning locally on the OT-MICROSERVICES/frontend repository using Trivy.

---

## 2. Objective

This Proof of Concept (POC) validates:

Detection of vulnerabilities in npm dependencies

Identification of license compliance issues

Local security validation before CI integration

Developer-level security checks before pushing code

---

## 3. Prerequisites
Ensure the following tools are installed:
|Tool|Version|
|----|-------|
|Git|Latest|
|npm|Latest|
|Trivy|Latest|

---

## 4. Repository Setup
### Step 1: Clone the Repository
```bash
git clone https://github.com/OT-MICROSERVICES/frontend.git
cd frontend
```
### Step 2: Install Dependencies
```bash
npm install
```
This installs:

- Direct dependencies

- Transitive dependencies

- Generates package-lock.json (if not present)

---

## 5. Install Trivy (If Not Installed)
```bash
sudo apt update
sudo apt install trivy
```
Verify Installation:
```bash
trivy --version
```
## 6. Run Dependency Scan
From the project root directory (where package.json exists), run:
```bash
trivy fs --scanners vuln,license .
```
### Command Explanation
- `fs` → Scans local file system

- `--scanners vuln,license` → Enables vulnerability and license scanning

- `.` → Scans current directory

This will scan:

- package.json

- package-lock.json

- Direct dependencies

- Transitive dependencies

---
## 7. Severity Filtering (Optional but Recommended)
####
```bash
trivy fs --scanners vuln --severity HIGH,CRITICAL .
```
#### Fail Command If HIGH/CRITICAL Vulnerabilities Found
```bash
trivy fs --scanners vuln --severity HIGH,CRITICAL --exit-code 1 .
```
---

## 8. Expected Output
The scan report will display:

- Vulnerability ID (CVE)

- Affected package name

- Installed version

- Fixed version (if available)

- Severity level

- License type (if license scan enabled)

output format:
```bash

```
## 9. Conclusion

This POC confirms that dependency scanning can be performed directly on the OT-MICROSERVICES/frontend repository using Trivy without CI integration.

This approach helps developers:

- Identify vulnerabilities early

- Ensure license compliance

- Validate security before pushing code

---

## 10. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) | 
