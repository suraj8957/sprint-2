# Python CI Checks – Bug Analysis POC
(Attendance API & Notification Worker)

---

## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 07-03-2026 | v1.0 | Suraj Tripathi | 07-03-2026 | | Aniruddh | Shreya S | Ashwani |

---

## Table of Contents

1. [Introduction](#1-introduction)  
2. [Objective of POC](#2-objective-of-poc)  
3. [Repositories Used](#3-repositories-used)  
4. [Tools Used for Bug Analysis](#4-tools-used-for-bug-analysis)  
5. [Environment Setup](#5-environment-setup)  
6. [Running Bug Analysis on Attendance API](#6-running-bug-analysis-on-attendance-api)  
7. [Running Bug Analysis on Notification Worker](#7-running-bug-analysis-on-notification-worker)  
8. [POC Workflow](#8-poc-workflow)  
9. [Expected Output](#9-expected-output)  
10. [Conclusion](#10-conclusion)  
11. [Contact Information](#11-contact-information)  
12. [References](#12-references)  

---

## 1. Introduction

Continuous Integration (CI) pipelines typically run automated checks to validate code quality, detect bugs, and enforce coding standards.

Before integrating these checks into CI pipelines, it is recommended to validate them manually using a Proof of Concept (POC).

This document demonstrates how to perform **manual bug analysis for Python microservices** using static analysis tools.

The POC is executed on the following services:

- Attendance API
- Notification Worker

These services are part of the **OT-MICROSERVICES architecture**.

---

## 2. Objective of POC

The objective of this POC is to manually validate bug detection tools before integrating them into CI pipelines.

The POC focuses on detecting:

- Code quality issues
- Logical bugs
- Style violations
- Security vulnerabilities

The results will help determine the appropriate tools to be integrated into the CI pipeline.

---

## 3. Repositories Used

| Service | Repository |
|------|------|
| Attendance API | https://github.com/OT-MICROSERVICES/attendance-api |
| Notification Worker | https://github.com/OT-MICROSERVICES/notification-worker |

These repositories contain Python-based microservices responsible for handling attendance tracking and notification processing.

---

## 4. Tools Used for Bug Analysis

The following static analysis tools are used in this POC.

| Tool | Purpose |
|-----|-----|
| Pylint | Detects bugs, code smells, and coding standard violations |
| Flake8 | Performs style checking and linting |
| Bandit | Detects security vulnerabilities in Python code |

These tools are commonly used in Python development environments and can easily be integrated into CI pipelines.

---

## 5. Environment Setup

### Step 1 – Clone Repositories

Clone the repositories to your local system.

```bash
git clone https://github.com/OT-MICROSERVICES/attendance-api.git
git clone https://github.com/OT-MICROSERVICES/notification-worker.git
```
Navigate to the attendance repository.
```bash
cd attendance-api
```
### Step 2 – Create Virtual Environment
Create a Python virtual environment.
```bash
python3 -m venv venv
```
Activate the environment.
```bash
source venv/bin/activate
```
<img width="1853" height="82" alt="image" src="https://github.com/user-attachments/assets/8b08bf15-a344-4cae-88b6-fd67adc63185" />

### Step 3 – Install Bug Analysis Tools
Install the required static analysis tools.
```bash
pip install pylint flake8 bandit
```
Verify installation.
```bash
pylint --version
flake8 --version
bandit --version
```
<img width="1853" height="203" alt="image" src="https://github.com/user-attachments/assets/ddd73028-460d-4229-84cc-64caa7ad25fd" />

---

## 6. Running Bug Analysis on Attendance API
Navigate to the repository.
```bash
cd attendance-api
```
##### Run Pylint
```bash
pylint .
```
Pylint analyzes the codebase and reports:
- code smells

- unused variables

- missing documentation

- logical issues

Output:
<img width="1848" height="600" alt="image" src="https://github.com/user-attachments/assets/8527e736-c1e2-43ec-8994-6c1d48f08a3e" />


##### Run Flake8
```bash
flake8 .
```
Flake8 checks coding style and formatting.

Output
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/319d9759-ebc1-4643-990a-285033cf25cb" />


##### Run Bandit Security Scan
```bash
bandit -r .
```
Bandit scans the code for potential security issues.

Output
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ccd6e4aa-3cc3-41df-a564-8f3d071e15f3" />


---

## 7. Running Bug Analysis on Notification Worker
Navigate to the notification worker repository.
```bash
cd ../notification-worker
```
Run the same analysis tools.
##### Run Pylint
```bash
pylint .
```
<img width="1906" height="331" alt="image" src="https://github.com/user-attachments/assets/8dc31ae1-e3e9-460c-894d-2bc445f8590e" />


##### Run Flake8
```bash
flake8 .
```
<img width="1920" height="490" alt="image" src="https://github.com/user-attachments/assets/fbcb63b7-7831-4506-a31c-530cc6b85970" />

##### Run Bandit
```bash
bandit -r .
```
<img width="1920" height="602" alt="image" src="https://github.com/user-attachments/assets/412cdfc6-8270-4a38-8832-53f8d172c745" />

This validates bug detection and security scanning for the notification worker service.

---
## 8. POC Workflow

<img width="959" height="318" alt="_- visual selection (19)" src="https://github.com/user-attachments/assets/0597625a-722e-40b3-81f4-16d4b7e6fc87" />

---

## 9. Expected Output
| Tool   | Purpose                     | Expected Result               |
| ------ | --------------------------- | ----------------------------- |
| Pylint | Detect bugs and code smells | Warnings and suggestions      |
| Flake8 | Style validation            | Style errors if present       |
| Bandit | Security scanning           | Security warnings if detected |

Developers should resolve critical issues before committing code.

---

## 10. Conclusion
This POC validates that Python static analysis tools can be executed manually on the following microservices:

- Attendance API

- Notification Worker

The tools successfully detect:

- coding standard violations

- potential bugs

- security issues

Based on this validation, the recommended CI tool stack is:

**Primary Tool:** SonarQube
Supporting Tools
- Pylint

- Flake8

- Bandit

Together, these tools provide comprehensive Python code quality analysis and can be integrated into CI pipelines for automated validation.

---

## 11. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |


---

## 12. References
| Resource             | Link                                                               |
| -------------------- | ------------------------------------------------------------------ |
| Python Documentation | [https://docs.python.org/3/](https://docs.python.org/3/)           |
| Pylint               | [https://pylint.org](https://pylint.org)                           |
| Flake8               | [https://flake8.pycqa.org](https://flake8.pycqa.org)               |
| Bandit               | [https://bandit.readthedocs.io](https://bandit.readthedocs.io)     |
| SonarQube            | [https://docs.sonarqube.org](https://docs.sonarqube.org)           |
| GitHub Actions       | [https://docs.github.com/actions](https://docs.github.com/actions) |

---
