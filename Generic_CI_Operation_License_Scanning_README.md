# Generic CI Operation – License Scanning Documentation
---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 12-02-2026 | v1.0 | Suraj Tripathi | 12-02-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---
# #Table of Contents

1. [Introduction](#introduction)
2. [What is License Scanning?](#what-is-license-scanning)
3. [Why License Scanning is Important](#why-license-scanning-is-important)
4. [Common License Types](#common-license-types)
5. [License Scanning Workflow](#license-scanning-workflow)
6. [Types of License Scanning](#types-of-license-scanning)
7. [Popular License Scanning Tools](#popular-license-scanning-tools)
8. [Tools Comparison](#tools-comparison)
9. [Advantages](#advantages)
10. [Best Practices](#best-practices)
11. [Advanced Implementation](#advanced-implementation)
12. [Challenges](#challenges)
13. [Recommendation & Conclusion](#recommendation--conclusion)
14. [Contact Information](#contact-information)
15. [References](#references)
---
## 1. Introduction:
In modern CI/CD pipelines, organizations use multiple open-source libraries and third-party dependencies. Every dependency comes with a software license (MIT, Apache, GPL, etc.), which defines how it can be used, modified, and distributed.

License Scanning in CI ensures that:

- No prohibited licenses are used

- Legal risks are minimized

- Compliance is automated before production deployment

License scanning is part of DevSecOps practices and is integrated into Continuous Integration pipelines.

---

## 2️. What is License Scanning?
License scanning is an automated process that:

- Detects open-source dependencies in a project

- Identifies their licenses

- Compares them against company compliance policies

- Fails the CI build if non-compliant licenses are detected

It works by analyzing:

- package.json

- pom.xml

- requirements.txt

- go.mod

- Docker images

- SBOM (Software Bill of Materials)

---
## 3. Why License Scanning is Important?
|                |              |
|----------------|--------------|
| Legal Protection | Avoid lawsuits due to GPL/copyleft violations. |
| Compliance     |   Ensure company policy adherence (e.g., only MIT/Apache allowed). |
| Risk Reduction |   Identify high-risk licenses early in development. |
| Automation     |Eliminate manual legal reviews for every dependency.  |
|Enterprise Governance|Maintain audit logs and compliance reports.|

---

## 4. Common License Types

|License|Type|Risk Level|Notes|
|-------|----|----------|-----|
|MIT|Permissive|Low|Commercial use allowed|
|Apache 2.0|Permissive|Low|Patent protection included|
|BSD|Permissive|Low|Similar to MIT|
|GPL v3|Copyleft|High|Must open-source derivative work|
|LGPL|Weak Copyleft|Medium|Linking allowed|
|MPL|Weak Copyleft|Medium|File-level copyleft|

---

## 5. License Scanning Workflow Diagram

<img width="792" height="612" alt="_- visual selection (13)" src="https://github.com/user-attachments/assets/60682505-434d-446a-ac37-a0d851b59b91" />

### Step-by-Step Workflow
- Developer pushes code to Git repository

- CI pipeline triggers

- Dependency installation step

- License scanning tool runs

- Policy engine checks license compliance

- Generate report

- If violation → Build fails

- If compliant → Continue deployment

---

## 6. Types of License Scanning

|Types| Discription|
|Source Code Scanning|Scans source files and dependency manifests.|
|Binary Scanning|Scans compiled artifacts.|
|Container Image Scanning|Scans Docker images.|
|SBOM-Based Scanning|Uses Software Bill of Materials.|

---

## 7. Popular License Scanning Tools

| Tool Name                     | Type / Model        | Key Features                                      | Pricing Model              |
|--------------------------------|---------------------|--------------------------------------------------|----------------------------|
| **Black Duck**                | Enterprise-grade    | Advanced policy management, Deep dependency analysis | Paid                       |
| **FOSSA**                     | Cloud-based         | CI integrations, License & vulnerability scanning | Paid (Free trial available) |
| **Snyk**                      | Developer-friendly  | License + security scanning, GitHub integration | Freemium                   |
| **OWASP Dependency-Check**    | Open-source         | Mainly vulnerability scanning, Basic license detection | Free                       |
| **WhiteSource (Mend)**        | Enterprise-focused  | Enterprise compliance, Automated policy enforcement | Paid                       |
| **Trivy**                     | Open-source         | Container + license scanning, Lightweight, CI friendly | Free                       |

---

## 8. Tools Comparison
## License Scanning Tools Comparison

| Tool       | Type        | License Detection | CI Integration | Cost     | Best For            |
|------------|------------|------------------|---------------|----------|---------------------|
| Black Duck | Enterprise | Advanced         | Yes           | Paid     | Large Enterprises   |
| FOSSA      | SaaS       | Advanced         | Yes           | Paid     | Compliance Teams    |
| Snyk       | Dev-first  | Good             | Yes           | Freemium | DevOps Teams        |
| Trivy      | Open-source| Good             | Yes           | Free     | Cloud-Native Teams  |
| OWASP DC   | Open-source| Limited          | Yes           | Free     | Small Teams         

---

## 9. Advantages of License Scanning

- Automated compliance
- Legal risk mitigation
- CI/CD integration
- Policy enforcement
- Audit readiness
- Faster release cycles
- Transparency via SBOM

## 10. License Scanning – Best Practices

| #  | Best Practice                          | Description                                                                 |
|----|------------------------------------------|-----------------------------------------------------------------------------|
| 1  | Define Allowed & Denied License List     | Create an internal compliance policy specifying approved and restricted licenses. |
| 2  | Integrate Early (Shift Left)             | Run license scanning during Pull Request (PR) stage to detect issues early. |
| 3  | Automate Policy Enforcement              | Configure CI pipeline to automatically fail builds on license violations. |
| 4  | Maintain SBOM                            | Maintain an up-to-date Software Bill of Materials (SBOM) for all dependencies. |
| 5  | Monitor Continuously                     | Perform periodic scans even after production release to detect new risks. |
| 6  | Combine with Vulnerability Scanning      | Use integrated DevSecOps tools to scan for both license and security issues. |

---
## 11. Advanced Implementation
### CI Integration Example (GitHub Actions)
```bash
name: License Scan

on: [push]

jobs:
  license-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run Trivy License Scan
        run: trivy fs --license .
```
### Enterprise Policy Example
- Allowed: MIT, Apache-2.0, BSD

- Review Required: LGPL, MPL

- Blocked: GPL-3.0

---

## 12. Challenges
- False positives

- Transitive dependencies

- License changes over time

- Manual review required sometimes

---

## 13. Recommendation & Conclusion
For a generic CI operation in modern cloud-native environments:

- If budget is available → Black Duck or FOSSA

- For developer-first approach → Snyk

- For open-source, lightweight CI integration → Trivy

#### Final Recommendation
For most DevOps teams (including startups and mid-size companies), I would choose:Trivy
##### Reason:
- Open-source

- Easy CI integration

- Container + license + vulnerability scanning

- Lightweight and fast

- Good community support

It provides a strong balance between functionality and cost efficiency.

---

## 14. Contact Information
| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

## 15. References

| Tool / Organization | Official Documentation Link |
|---------------------|-----------------------------|
| Black Duck | https://www.synopsys.com/software-integrity/security-testing/software-composition-analysis.html |
| FOSSA | https://docs.fossa.com/ |
| Snyk License Documentation | https://docs.snyk.io/scan-using-snyk/snyk-open-source/license-compliance |
| OWASP Dependency-Check | https://owasp.org/www-project-dependency-check/ |
| Aqua Security Trivy | https://aquasecurity.github.io/trivy/ |
| Open Source Initiative (OSI) | https://opensource.org/licenses |
