# React CI Checks – Dependency Scanning Document

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 12-02-2026 | v1.0 | Suraj Tripathi | 12-02-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---
## Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Dependency Scanning?](#2-what-is-dependency-scanning)  
3. [Why Dependency Scanning is Important](#3-why-dependency-scanning-is-important)  
   - [3.1 Security Risk Mitigation](#31-security-risk-mitigation)  
   - [3.2 License Compliance](#32-license-compliance)  
   - [3.3 CI/CD Governance](#33-cicd-governance)  
   - [3.4 DevSecOps Alignment](#34-devsecops-alignment)  
4. [Dependency Scanning Workflow in CI](#4-dependency-scanning-workflow-in-ci)  
5. [Tools for Dependency Scanning](#5-tools-for-dependency-scanning)  
   - [5.1 Snyk](#51-snyk)  
   - [5.2 OWASP Dependency-Check](#52-owasp-dependency-check)  
   - [5.3 Trivy](#53-trivy)  
   - [5.4 Black Duck](#54-black-duck)  
   - [5.5 Mend (WhiteSource)](#55-mend-whitesource)  
6. [Tool Comparison](#6-tool-comparison)  
7. [Advantages of Dependency Scanning](#7-advantages-of-dependency-scanning)  
8. [Best Practices](#8-best-practices)  
9. [Recommendation and Conclusion](#9-recommendation-and-conclusion)  
10. [Contact Information](#10-contact-information)  
11. [References](#11-references)  

---

## 1. Introduction

Modern React applications rely heavily on third-party npm packages to accelerate development. While dependencies improve productivity and reduce development time, they also introduce potential security vulnerabilities and license compliance risks.

Dependency scanning is implemented in the CI pipeline to automatically detect vulnerabilities and policy violations before code is merged or deployed.

This document provides detailed information about dependency scanning, its purpose, workflow, tools, comparison, advantages, best practices, and final recommendation.

---

## 2. What is Dependency Scanning?

Dependency scanning is a security practice that analyzes project dependencies (such as `package.json`, `package-lock.json`, and `yarn.lock`) to detect:

- Known security vulnerabilities (CVEs)
- Outdated or deprecated packages
- License compliance issues
- Risks in transitive dependencies

It ensures complete visibility into both direct and indirect dependencies used within the React application.

---

## 3. Why Dependency Scanning is Important

### 3.1 Security Risk Mitigation

React projects often include hundreds of dependencies. A single vulnerable package can expose the application to:

- Cross-Site Scripting (XSS)
- Remote Code Execution (RCE)
- Supply chain attacks
- Data breaches

### 3.2 License Compliance

Organizations may restrict the use of certain open-source licenses (e.g., GPL). Automated scanning ensures adherence to compliance policies.

### 3.3 CI/CD Governance

Integrating dependency scanning into CI ensures:

- Automated enforcement of security policies
- Prevention of insecure code merge
- Early detection of risks

### 3.4 DevSecOps Alignment

Shifts security left by detecting vulnerabilities during development rather than after deployment.

---

## 4. Dependency Scanning Workflow in CI
<img width="1034" height="450" alt="_- visual selection (14)" src="https://github.com/user-attachments/assets/c785d9d3-fd3c-4716-869d-1f29b52859a5" />


### Workflow Steps

1. Developer pushes code or creates a Pull Request.
2. CI pipeline is triggered automatically.
3. Dependencies are installed.
4. Dependency scanning tool analyzes project files.
5. A report is generated.
6. Pipeline fails if vulnerabilities exceed defined thresholds.
7. Code merges only if scan passes policy checks.

---

## 5. Tools for Dependency Scanning

### 5.1 Snyk

- Developer-friendly  
- Vulnerability and license scanning  
- Strong GitHub integration  
- Freemium model  

### 5.2 OWASP Dependency-Check

- Open-source  
- Vulnerability-focused scanning  
- CLI-based  
- Free  

### 5.3 Trivy

- Open-source and lightweight  
- Fast scanning  
- Supports vulnerability and license scanning  
- CI/CD friendly  

### 5.4 Black Duck

- Enterprise-grade solution  
- Advanced policy management  
- Deep dependency analysis  
- Paid tool  

### 5.5 Mend (WhiteSource)

- Enterprise compliance automation  
- Automated license governance  
- Paid solution  

---

## 6. Tool Comparison

| Tool | Vulnerability Scan | License Scan | CI Integration | Cost | Suitable For |
|------|-------------------|--------------|---------------|------|-------------|
| Snyk | Yes | Yes | Excellent | Freemium | Developer-focused teams |
| OWASP Dependency-Check | Yes | Basic | Good | Free | Small projects |
| Trivy | Yes | Yes | Very Good | Free | DevOps pipelines |
| Black Duck | Yes | Yes | Excellent | Paid | Enterprise |
| Mend | Yes | Yes | Excellent | Paid | Compliance-heavy organizations |

---

## 7. Advantages of Dependency Scanning

- Early vulnerability detection  
- Prevention of supply chain attacks  
- Automated license compliance  
- Improved security posture  
- CI/CD enforcement  
- Reduced production incidents  
- Better audit and compliance reporting  

---

## 8. Best Practices

- Enable scanning on every Pull Request  
- Block merge on High and Critical vulnerabilities  
- Maintain vulnerability baseline  
- Regularly update dependencies  
- Monitor transitive dependencies  
- Define organization-level license policies  
- Integrate with DevSecOps dashboards  
- Combine with automated dependency update tools  

---

## 9. Recommendation and Conclusion

For React CI environments, the recommended tool is:

### Trivy

#### Reasons:

- Open-source and cost-effective  
- Supports both vulnerability and license scanning  
- Easy integration into CI/CD pipelines  
- Fast and lightweight  
- Suitable for DevOps-driven teams  
- Scalable for future container scanning needs  

For enterprise-level policy management, Black Duck or Mend can be considered.

However, for most DevOps-oriented React projects, Trivy provides the best balance between security coverage, performance, and cost efficiency.

---

## 10. Contact Information

**Prepared By:**  
| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) | 

---

---

## 11. References

| Resource | Description | Official Link |
|----------|------------|---------------|
| Trivy Documentation | Official documentation for Trivy dependency and vulnerability scanning | https://aquasecurity.github.io/trivy/ |
| Snyk Documentation | Official Snyk security scanning documentation | https://docs.snyk.io/ |
| OWASP Dependency-Check | Official documentation for OWASP Dependency-Check | https://owasp.org/www-project-dependency-check/ |
| Black Duck Documentation | Synopsys Black Duck official documentation | https://www.synopsys.com/software-integrity/security-testing/software-composition-analysis.html |
| Mend Documentation | Official Mend (WhiteSource) documentation | https://docs.mend.io/ |
| React Official Documentation | Official React documentation | https://react.dev/ |

---
