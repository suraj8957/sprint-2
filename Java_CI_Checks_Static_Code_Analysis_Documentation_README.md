# Java CI Checks – Static Code Analysis Documentation

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |


---
# Table of Contents

- [1. Introduction](#1-introduction)
- [2. What is CI (Continuous Integration)?](#2-what-is-ci-continuous-integration)
  - [Basic CI Workflow](#basic-ci-workflow)
- [3. What is Static Code Analysis?](#3-what-is-static-code-analysis)
- [4. Why Static Code Analysis is Important?](#4-why-static-code-analysis-is-important)
  - [4.1 Early Bug Detection](#41-early-bug-detection)
  - [4.2 Security](#42-security)
  - [4.3 Maintainability](#43-maintainability)
  - [4.4 Standardization](#44-standardization)
  - [4.5 DevOps Quality Gate](#45-devops-quality-gate)
- [5. Static Code Analysis Workflow Diagram](#5-static-code-analysis-workflow-diagram)
- [6. Popular Static Code Analysis Tools for Java](#6-popular-static-code-analysis-tools-for-java)
  - [6.1 SonarQube](#61-sonarqube)
  - [6.2 Checkstyle](#62-checkstyle)
  - [6.3 PMD](#63-pmd)
  - [6.4 SpotBugs](#64-spotbugs)
  - [6.5 OWASP Dependency-Check](#65-owasp-dependency-check)
- [7. Tools Comparison](#7-tools-comparison)
- [8. Advantages of Static Code Analysis](#8-advantages-of-static-code-analysis)
- [9. Best Practices](#9-best-practices)
  - [9.1 Shift Left](#91-shift-left)
  - [9.2 Enforce Quality Gates](#92-enforce-quality-gates)
  - [9.3 Maintain Coverage Threshold](#93-maintain-coverage-threshold)
  - [9.4 Analyze Branches](#94-analyze-branches)
  - [9.5 Combine Tools](#95-combine-tools)
- [10. Advanced Concepts](#10-advanced-concepts)
- [11. Recommendation / Conclusion](#11-recommendation--conclusion)
  - [11.1 Primary Recommendation: SonarQube](#111-primary-recommendation-sonarqube)
  - [11.2 Additional Recommendation](#112-additional-recommendation)
- [12. Contact Information](#12-contact-information)
- [13. References](#13-references)

---
## 1. Introduction

In modern software development, writing code is not enough. We must ensure that:

- Code follows standards

- Code is secure

- Code has no bugs

- Code is maintainable

- Code quality remains high over time

This is where CI (Continuous Integration) Checks and Static Code Analysis come into the picture.

In Java projects (especially enterprise and microservices), static analysis is a mandatory DevOps practice integrated inside CI pipelines like:

- Jenkins

- GitHub Actions

- GitLab CI/CD

---

## 2. What is CI (Continuous Integration)?

Continuous Integration is a practice where:

- Developers push code frequently

- Code is automatically built

- Automated tests run

- Quality checks run

- Reports are generated

### Basic CI Workflow

<img width="768" height="462" alt="_- visual selection (16)" src="https://github.com/user-attachments/assets/b64464e2-948a-4c5a-bfd6-a8a8caa32396" />

---

## 3. What is Static Code Analysis?
Static Code Analysis is:

Static Code Analysis is an automated process of analyzing source code without executing it to detect bugs, vulnerabilities, and code smells.

It checks:
- Coding standards

- Complexity

- Duplicate code

- Null pointer risks

- Memory leaks

- Security vulnerabilities

- Hardcoded secrets

---

## 4. Why Static Code Analysis is Important?

### 4.1 Early Bug Detection
Fixing bugs early is cheaper than fixing in production.
### 4.2 Security
Detect:

- SQL Injection

- XSS

- Hardcoded credentials

- Weak cryptography

### 4.3 Maintainability

- Detect large classes

- Deep nesting

- High complexity

### 4.4 Standardization
Enforce company coding rules.

### 4.5 DevOps Quality Gate
Fail build if:

- Code coverage < 80%

- Vulnerabilities > 0

- Code smells > threshold

---

## 5. Static Code Analysis Workflow Diagram
```bash
        Developer
            ↓
        Git Push
            ↓
     CI Pipeline Trigger
            ↓
    ┌────────────────────┐
    │  Build (Maven)     │
    └────────────────────┘
            ↓
    ┌────────────────────┐
    │  Unit Testing      │
    └────────────────────┘
            ↓
    ┌────────────────────┐
    │ Static Analysis    │
    │ (SonarQube etc.)   │
    └────────────────────┘
            ↓
      Quality Gate
            ↓
   Pass  →  Merge
   Fail  →  Fix Code
```

---

## 6. Popular Static Code Analysis Tools for Java

### 6.1 SonarQube
Enterprise-level platform for:

- Bugs

- Vulnerabilities

- Code smells

- Coverage

- Duplications

- Quality Gates

Supports:

- Maven

- Gradle

- Jenkins

- GitHub Actions

### 6.2 Checkstyle

Focus:

- Coding standards

- Naming conventions

- Formatting rules

### 6.3 PMD

Detects:

- Dead code

- Unused variables

- Empty catch blocks

### 6.4 SpotBugs

Detects:

- Null pointer dereference

- Bad practice patterns

- Security issues

### 6.5 OWASP Dependency-Check

Scans:

- Vulnerable libraries

- CVE vulnerabilities

---

## 7. Tools Comparison

| Tool | Focus | Security | UI Dashboard | CI Integration | Enterprise Ready |
|-----|------|----------|--------------|---------------|-----------------|
| SonarQube | Full Quality | Yes | Yes | Yes | Yes |
| Checkstyle | Coding Standards | No | No | Yes | No |
| PMD | Code Smells | Partial | No | Yes | No |
| SpotBugs | Bug Detection | Yes | No | Yes | No |
| OWASP Dependency Check | Dependency Security | Yes | Basic | Yes | Yes |


---

## 8. Advantages of Static Code Analysis
- Improves code quality

- Reduces technical debt

- Prevents production failures

- Improves team productivity

- Enforces DevSecOps

- Automated governance

---
## 9. Best Practices
### 9.1 Shift Left
Run static analysis:

- On every commit

- On every pull request

### 9.2 Enforce Quality Gates

- Never merge if gate fails.

### 9.3 Maintain Coverage Threshold

- Minimum 80%.

### 9.4 Analyze Branches

Use:

- Feature branch analysis

- Main branch analysis

### 9.5 Combine Tools

Recommended stack:

- SonarQube → Overall quality

- OWASP Dependency-Check → Security

- Checkstyle → Coding discipline

---

## 10. Advanced Concepts

- JaCoCo integration for coverage

- Pull request decoration

- Custom rule creation

- Multi-module project scanning

- Dockerized SonarQube

- DevSecOps integration

- Technical Debt ratio monitoring

- SAST integration

- Secret scanning

---

## 11. Recommendation / Conclusion

For Java CI Static Code Analysis:

### 11.1 Primary Recommendation: SonarQube
Reasons:

- Complete code quality platform

- Security + Bugs + Coverage

- Quality Gates enforcement

- Enterprise ready

- CI/CD integration support

- Excellent reporting and dashboards

### 11.2 Additional Recommendation
Combine with:

- OWASP Dependency-Check for dependency security

---
## 12. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

---

## 13. References

| Category | Organization / Tool | Description | Official Link |
|----------|--------------------|-------------|----------------|
| Code Quality | SonarQube | Official SonarQube Documentation & User Guide | https://docs.sonarsource.com/sonarqube/ |
| Security | OWASP | OWASP Main Website & Security Projects | https://owasp.org/ |
| Dependency Security | OWASP Dependency-Check | OWASP Dependency-Check Documentation | https://owasp.org/www-project-dependency-check/ |
| Build Tool | Apache Maven | Maven Official Documentation | https://maven.apache.org/ |
| CI/CD | Jenkins | Jenkins Official Documentation | https://www.jenkins.io/doc/ |

---
