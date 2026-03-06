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

- [Prerequisites](#1-prerequisites)
- [Clone Repository](#2-clone-repository)
- [Project Structure](#3-project-structure)
- [Install Dependencies](#4-install-dependencies)
- [Run All Unit Tests](#5-run-all-unit-tests)
- [Run Tests with Verbose Output](#6-run-tests-with-verbose-output)
- [Exclude Certain Packages (Optional)](#7-exclude-certain-packages-optional)
- [Run Tests with Race Detection](#8-run-tests-with-race-detection)
- [Generate Code Coverage](#9-generate-code-coverage)
- [Generate Coverage Report File](#10-generate-coverage-report-file)
- [View Coverage in Browser](#11-view-coverage-in-browser)
- [Run Tests for Specific Package](#12-run-tests-for-specific-package)
- [Run a Specific Test Function](#13-run-a-specific-test-function)
- [Cleaning Test Cache](#14-cleaning-test-cache)
- [Contact Information](#15-contact-information)

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
```
<img width="1764" height="79" alt="image" src="https://github.com/user-attachments/assets/bb43a49b-5456-4d5f-abb1-aee34198096a" />

```bash
git --version
```
<img width="1764" height="79" alt="image" src="https://github.com/user-attachments/assets/d2a4cdfe-5368-4d3e-bbcf-eb8b754c000f" />

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
Unit tests are present in multiple packages, such as:
- api

- client

- config

- middleware

- routes

Test files follow the Go naming convention:
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
<img width="1848" height="781" alt="image" src="https://github.com/user-attachments/assets/4e347132-54e5-4d78-9c20-521018d7099b" />


---

## 5. Run All Unit Tests
Execute tests for all packages.
```bash
go test ./...
```
Output:
<img width="1854" height="999" alt="image" src="https://github.com/user-attachments/assets/9a4919c6-12d5-489c-a7f4-36fdab18e71b" />


---
## 6. Run Tests with Verbose Output
```bash
go test -v ./...
```
Output:
<img width="1854" height="999" alt="image" src="https://github.com/user-attachments/assets/c95126d3-d56c-4f7d-b8df-0ac4e0ea779e" />


---
## 7. Exclude Certain Packages (Optional)
Sometimes we exclude packages like docs or models during testing.
```bash
go test $(go list ./... | grep -v docs | grep -v model)
```
<img width="1854" height="999" alt="image" src="https://github.com/user-attachments/assets/39a087a2-6b22-4e89-be0e-efb874a4fe04" />

---
## 8. Run Tests with Race Detection
Detect race conditions in concurrent code.
```bash
go test -race ./...
```
<img width="1854" height="999" alt="image" src="https://github.com/user-attachments/assets/d67d4811-289c-4ead-b61f-b98309ecbedb" />

---
## 9. Generate Code Coverage
Run tests with coverage.
```bash
go test -cover ./...
```
output:
<img width="1861" height="990" alt="image" src="https://github.com/user-attachments/assets/0b4eb270-1e07-4626-8881-aebec5247a0d" />
<img width="1861" height="1002" alt="image" src="https://github.com/user-attachments/assets/d33bd844-8730-491e-a7b4-8a0def43153f" />

---

## 10. Generate Coverage Report File
```bash
go test ./... -coverprofile=cover.out
```
<img width="1861" height="1002" alt="image" src="https://github.com/user-attachments/assets/45a6a3f6-bf0b-4cf4-ad2e-c23534e7a59a" />
<img width="1861" height="1002" alt="image" src="https://github.com/user-attachments/assets/4a4a6385-5f7b-4d4f-995e-52c431fb4f01" />



---
## 11. View Coverage in Browser
```bash
go tool cover -html=cover.out
```
This opens an HTML coverage report in the browser.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/391ab90d-1069-41db-98d9-4ba5694244c4" />


---
## 12. Run Tests for Specific Package
for api package:
```bash
go test ./api
```
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/19e5cde5-0447-4666-a5d2-1ccb0e3c5c0b" />


---
## 13. Run a Specific Test Function
```bash
go test -run TestEmployeeSearch ./api
```
<img width="1861" height="68" alt="image" src="https://github.com/user-attachments/assets/10c62bb8-54b6-4bc6-b80f-896c6d39e368" />

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

