# Static Code Analysis POC – Using SonarQube

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---
## Table of Contents

- [1. Objective](#1-objective)
- [2. Prerequisites](#2-prerequisites)
- [3. Implementation Steps](#3-implementation-steps)
  - [3.1 Clone the Repository](#31-clone-the-repository)
  - [3.2 Verify Project Build](#32-verify-project-build)
  - [3.3 Start SonarQube Server](#33-start-sonarqube-server)
  - [3.4 Access SonarQube Dashboard](#34-access-sonarqube-dashboard)
  - [3.5 Run SonarQube Analysis](#35-run-sonarqube-analysis)
  - [3.6 Review SonarQube Report](#36-review-sonarqube-report)
  - [3.7 Configure Quality Gate](#37-configure-quality-gate-recommended)
- [4. Re-Scan After Fixes](#4-re-scan-after-fixes)
- [5. Conclusion](#5-conclusion)
- [6. Contact Information](#6-contact-information)

---

## 1. Objective

This document provides step-by-step instructions to perform Static Code Analysis using SonarQube on the following GitHub repository.  

Repository:
https://github.com/OT-MICROSERVICES/salary-api.git

The goal is to analyze:

- Bugs
- Vulnerabilities
- Code Smells
- Code Coverage
- Duplications
- Technical Debt
- Quality Gate Status

---

## 2. Prerequisites

Ensure the following tools are installed:

| Tool | Required Version | Check Command |
|------|------------------|--------------|
| Java | 17+ | `java -version` |
| Maven | 3.8+ | `mvn -version` |
| Git | Latest | `git --version` |
| SonarQube | 9.x or higher | Running locally |

---
## 3. Implementation Steps
### 3.1: Clone the Repository

```bash
git clone https://github.com/OT-MICROSERVICES/salary-api.git
cd salary-api
```
### 3.2: Verify Project Build
Ensure the project builds successfully before analysis:
```
mvn clean install
```
or 
```
mvn clean install -DskipTests
```

If the build fails, resolve dependency or configuration issues before proceeding.

### 3.3: Start SonarQube Server

```bash
sudo -u sonar /opt/sonarqube/bin/linux-x86-64/sonar.sh start
```

### 3.4: Access SonarQube Dashboard
Open in browser:
```bash
http://localhost:9000
```
Default Credentials:
```bash
Username: admin
Password: admin
```
After login:

 - Go to My Account

- Click Security

- Generate a new Token

- Copy the generated token
<img width="1844" height="453" alt="image" src="https://github.com/user-attachments/assets/32b930b4-ba89-4a02-a000-af8bae09fb82" />


### 3.5: Run SonarQube Analysis

From the root directory of salary-api, execute:
```bash
mvn clean verify sonar:sonar \
-Dsonar.projectKey=salary-api \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=YOUR_GENERATED_TOKEN
```
Replace YOUR_GENERATED_TOKEN with your actual token.

### 3.6: Review SonarQube Report
After successful execution:

- Open Sonar Dashboard

- Select project: salary-api

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ef29ea8f-1224-4252-b4ec-5d25605d0a42" />


Review the following metrics:
| Metric          | Description                   |
| --------------- | ----------------------------- |
| Bugs            | Functional issues in code     |
| Vulnerabilities | Security risks                |
| Code Smells     | Maintainability issues        |
| Coverage        | Unit test coverage percentage |
| Duplications    | Duplicate code blocks         |
| Technical Debt  | Estimated fix effort          |

### 3.7: Configure Quality Gate (Recommended)
Create a Quality Gate with conditions such as:

- Coverage < 80% → Fail

- Bugs > 0 → Fail

- Vulnerabilities > 0 → Fail

- Duplications > 3% → Fail

Assign the Quality Gate to salary-api.

Re-run scan to verify the Quality Gate status.

## 4. Re-Scan After Fixes

After fixing issues:
```bash
mvn clean verify sonar:sonar \
-Dsonar.projectKey=salary-api \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=YOUR_GENERATED_TOKEN
```  
Ensure Quality Gate shows Passed.

## 5. Conclusion
SonarQube provides:

- Centralized dashboard

- Code quality visibility

- Security vulnerability detection

- Quality Gate enforcement

- CI/CD integration readiness

This POC demonstrates static code analysis using SonarQube for enterprise-grade Java projects.

## 6. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

