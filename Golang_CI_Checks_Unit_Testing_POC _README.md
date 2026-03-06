# GoLang Unit Testing POC – employee-api

This document demonstrates how to perform a **Unit Testing Proof of Concept (POC)** on the `employee-api` Go microservice repository.

Repository:
https://github.com/OT-MICROSERVICES/employee-api

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |

---

## Table of Contents

1. [Prerequisites](#1-prerequisites)
2. [Clone Repository](#2-clone-repository)
3. [Project Structure](#3-project-structure)
4. [Install Dependencies](#4-install-dependencies)
5. [Run All Unit Tests](#5-run-all-unit-tests)
6. [Run Tests with Verbose Output](#6-run-tests-with-verbose-output)
7. [Exclude Certain Packages (Optional)](#7-exclude-certain-packages-optional)
8. [Run Tests with Race Detection](#8-run-tests-with-race-detection)
9. [Generate Code Coverage](#9-generate-code-coverage)
10. [Generate Coverage Report File](#10-generate-coverage-report-file)
11. [View Coverage in Browser](#11-view-coverage-in-browser)
12. [Run Tests for Specific Package](#12-run-tests-for-specific-package)
13. [Run a Specific Test Function](#13-run-a-specific-test-function)
14. [Cleaning Test Cache](#14-cleaning-test-cache)
15. [Contact Information](#15-contact-information)
---

# 1. Prerequisites

Ensure the following tools are installed:

| Tool | Version |
|-----|--------|
| Go | >= 1.20 |
| Git | Latest |
| Make | Optional |

Verify installation:

```bash
go version
git --version

```

Example output:
```bash
go version go1.21 linux/amd64
```

---

## 2. Clone Repository
```bash
git clone https://github.com/OT-MICROSERVICES/employee-api.git
```
Navigate to repository:
```bash
cd employee-api
```
---

## 3. Project Structure
```
employee-api
│
├── api
├── client
├── config
├── middleware
├── routes
├── model
├── migration
├── main.go
├── go.mod
├── Dockerfile
└── Makefile
```
Unit tests are present in multiple packages such as:
- api

- client

- config

- middleware

- routes

Test files follow Go naming convention:
```
*_test.go
```
Example:
```
employee_handler_test.go
```

---

## 4. Install Dependencies
Download required Go modules.
```bash
go mod tidy
```
or
```bash
go mod download
```

---

## 5. Run All Unit Tests
Execute tests for all packages.
```bash
go test ./...
```
Output:

---
## 6. Run Tests with Verbose Output
```bash
go test -v ./...
```
Output:

---
## 7. Exclude Certain Packages (Optional)
Sometimes we exclude packages like docs or models during testing.
```bash
go test $(go list ./... | grep -v docs | grep -v model)
```
---
## 8. Run Tests with Race Detection
Detect race conditions in concurrent code.
```bash
go test -race ./...
```
---
## 9. Generate Code Coverage
Run tests with coverage.
```bash
go test -cover ./...
```
output:

---

## 10. Generate Coverage Report File
```bash
go test ./... -coverprofile=cover.out
```

---
## 11. View Coverage in Browser
```bash
go tool cover -html=cover.out
```
This opens an HTML coverage report in the browser.

---
## 12. Run Tests for Specific Package
for api package:
```bash
go test ./api
```

---
## 13. Run a Specific Test Function
```bash
go test -run TestEmployeeSearch ./api
```

---

## 14. Cleaning Test Cache
If tests behave unexpectedly, clear Go test cache.
```bash
go clean -testcache
```

---
## 15. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |

