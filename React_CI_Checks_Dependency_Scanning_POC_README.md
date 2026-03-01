# React Dependency Scanning – POC
---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---
## Table of Contents

1. [Introduction](#1-introduction)  
2. [Objective](#2-objective)  
3. [Prerequisites](#3-prerequisites)  
4. [Repository Setup](#4-repository-setup)  
   - [Step 1: Clone the Repository](#step-1-clone-the-repository)  
   - [Step 2: Install Dependencies](#step-2-install-dependencies)  
5. [Install Trivy (If Not Installed)](#5-install-trivy-if-not-installed)  
6. [Run Dependency Scan](#6-run-dependency-scan)  
   - [Command Explanation](#command-explanation)  
7. [Severity Filtering (Optional but Recommended)](#7-severity-filtering-optional-but-recommended)  
8. [Expected Output](#8-expected-output)  
9. [Conclusion](#9-conclusion)  
10. [Contact Information](#10-contact-information)  
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
<img width="1860" height="613" alt="image" src="https://github.com/user-attachments/assets/5a07be19-7cf0-4b44-b41a-16f1c736fc57" />

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
<img width="1884" height="455" alt="image" src="https://github.com/user-attachments/assets/9e8fc5ad-657e-49c6-9e1d-6228124ab87c" />

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
┌────────────────────────────┬────────────────┬──────────┬────────┬───────────────────┬───────────────────────────────────────────┬──────────────────────────────────────────────────────────────┐
│          Library           │ Vulnerability  │ Severity │ Status │ Installed Version │               Fixed Version               │                            Title                             │
├────────────────────────────┼────────────────┼──────────┼────────┼───────────────────┼───────────────────────────────────────────┼──────────────────────────────────────────────────────────────┤
│ golang.org/x/crypto        │ CVE-2024-45337 │ CRITICAL │ fixed  │ v0.9.0            │ 0.31.0                                    │ golang.org/x/crypto/ssh: Misuse of                           │
│                            │                │          │        │                   │                                           │ ServerConfig.PublicKeyCallback may cause authorization       │
│                            │                │          │        │                   │                                           │ bypass in golang.org/x/crypto                                │
│                            │                │          │        │                   │                                           │ https://avd.aquasec.com/nvd/cve-2024-45337                   │
│                            ├────────────────┼──────────┤        │                   ├───────────────────────────────────────────┼──────────────────────────────────────────────────────────────┤
│                            │ CVE-2025-22869 │ HIGH     │        │                   │ 0.35.0                                    │ golang.org/x/crypto/ssh: Denial of Service in the Key        │
│                            │                │          │        │                   │                                           │ Exchange of golang.org/x/crypto/ssh                          │
│                            │                │          │        │                   │                                           │ https://avd.aquasec.com/nvd/cve-2025-22869                   │
│                            ├────────────────┼──────────┤        │                   ├─────────────────────────────────────
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
