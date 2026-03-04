# Static Code Analysis POC – Using SonarQube

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |
---


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

### Step 1: Clone the Repository

```bash
git clone https://github.com/OT-MICROSERVICES/salary-api.git
cd salary-api
```
### Step 2: Verify Project Build
Ensure the project builds successfully before analysis:
```bash
mvn clean install
```
If the build fails, resolve dependency or configuration issues before proceeding.

### Step 3: Start SonarQube Server

```bash
cd sonarqube/bin/linux-x86-64
./sonar.sh start
```

### Step 4: Access SonarQube Dashboard
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

### Step 5: Run SonarQube Analysis

From the root directory of salary-api, execute:
```bash
mvn clean verify sonar:sonar \
-Dsonar.projectKey=salary-api \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=YOUR_GENERATED_TOKEN
```
Replace YOUR_GENERATED_TOKEN with your actual token.

### Step 6: Review SonarQube Report
After successful execution:

- Open Sonar Dashboard

- Select project: salary-api

Review the following metrics:
| Metric          | Description                   |
| --------------- | ----------------------------- |
| Bugs            | Functional issues in code     |
| Vulnerabilities | Security risks                |
| Code Smells     | Maintainability issues        |
| Coverage        | Unit test coverage percentage |
| Duplications    | Duplicate code blocks         |
| Technical Debt  | Estimated fix effort          |

### Step 7: Configure Quality Gate (Recommended)
Create a Quality Gate with conditions such as:

- Coverage < 80% → Fail

- Bugs > 0 → Fail

- Vulnerabilities > 0 → Fail

- Duplications > 3% → Fail

Assign the Quality Gate to salary-api.

Re-run scan to verify Quality Gate status.

#### Re-Scan After Fixes
After fixing issues:
```bash
mvn clean verify sonar:sonar \
-Dsonar.projectKey=salary-api \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.login=YOUR_GENERATED_TOKEN
```
Ensure Quality Gate shows Passed.

## Conclusion
SonarQube provides:

- Centralized dashboard

- Code quality visibility

- Security vulnerability detection

- Quality Gate enforcement

- CI/CD integration readiness

This POC demonstrates static code analysis using SonarQube for enterprise-grade Java projects.

## Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

