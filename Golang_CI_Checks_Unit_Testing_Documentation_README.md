#   GoLang CI Checks – Unit Testing Documentation

---
## Document Details

| Author | Created on | Version | Last updated by | Last edited on | Pre Reviewer | L0 Reviewer | L1 Reviewer | L2 Reviewer |
|--------|------------|---------|-----------------|----------------|--------------|-------------|-------------|-------------|
| Suraj Tripathi | 1-03-2026 | v1.0 | Suraj Tripathi | 1-03-2026 |              | Aniruddh    | Shreya S    | Ashwani |
---
## Table of Contents

1. [Introduction](#1-introduction)
2. [What is Unit Testing](#2-what-is-unit-testing)
3. [Why Unit Testing is Important](#3-why-unit-testing-is-important)
4. [Unit Testing in CI/CD Pipeline](#4-unit-testing-in-cicd-pipeline)
5. [Unit Testing Workflow](#5-unit-testing-workflow)
6. [Built-in GoLang Testing Framework](#6-built-in-golang-testing-framework)
7. [Basic Unit Test Example](#7-basic-unit-test-example)
8. [GoLang Unit Testing Commands](#8-golang-unit-testing-commands)
9. [Code Coverage](#9-code-coverage)
10. [Tools for GoLang Unit Testing](#10-tools-for-golang-unit-testing)
11. [Tool Comparison](#11-tool-comparison)
12. [Advantages of Unit Testing](#12-advantages-of-unit-testing)
13. [Best Practices for Go Unit Testing](#13-best-practices-for-go-unit-testing)
14. [Common Mistakes](#14-common-mistakes)
15. [Recommendation / Conclusion](#15-recommendation--conclusion)
16. [References](#16-references)
17. [Contact Information](#17-contact-information)

---

## 1. Introduction
Modern software development follows CI/CD (Continuous Integration / Continuous Deployment) practices to ensure that code changes are tested automatically before they are merged into the main codebase.

One of the most important CI checks is Unit Testing.

Unit testing ensures that individual components of the application work correctly before integrating them with other components.

In GoLang, unit testing is built-in, meaning Go provides native support for writing and running tests using the testing package.

This document explains:

- What Unit Testing is

- Why it is important

- How it works in GoLang

- Tools available

- Implementation example

- CI integration

Best practices

This guide progresses from basic concepts to advanced CI implementation.

---
## 2. What is Unit Testing?

Unit Testing is a software testing method where individual functions or modules of an application are tested independently.

A unit typically refers to:

- A function

- A method

- A module

- A small component of code

#### Example
Suppose we have a function:
```
func Add(a int, b int) int {
    return a + b
}
```
A unit test will verify:
```
Add(2,3) = 5
Add(5,5) = 10
```
If the output is incorrect, the test fails.

---

## 3. Why Unit Testing is Important
Benefits

- Early Bug Detection

- Code Reliability

- Faster Development

- Safe Refactoring

- Improved Code Quality

#### Example
Without unit testing:
```
Developer writes code
Code pushed to repository
Bug discovered in production
```
With unit testing:
```
Developer writes code
Unit tests executed in CI
Bug detected before merge
```
This prevents broken code from entering production.

---

## 4. Unit Testing in CI/CD Pipeline
Unit tests are executed automatically whenever code is pushed.

CI Pipeline Flow
```
Developer writes code
        │
        ▼
Code pushed to Git repository
        │
        ▼
CI pipeline triggered
        │
        ▼
Code Build
        │
        ▼
Unit Tests Run
        │
        ▼
Test Pass → Continue pipeline
Test Fail → Pipeline stops
```
---

## 5. Unit Testing Workflow
#### Step-by-Step Workflow
<img width="768" height="486" alt="_- visual selection (17)" src="https://github.com/user-attachments/assets/71aa17f7-1c84-4348-90a0-b091265a2684" />

#### Architecture Workflow Diagram
```
                +------------------+
                |   Developer      |
                +--------+---------+
                         |
                         |
                         v
                +------------------+
                |   Git Repository |
                +--------+---------+
                         |
                         |
                         v
                +------------------+
                |   CI Pipeline    |
                | (Jenkins/GitHub) |
                +--------+---------+
                         |
                         |
                         v
                +------------------+
                |   Run Unit Tests |
                +--------+---------+
                         |
                +--------+--------+
                |                 |
                v                 v
          Tests Pass          Tests Fail
              |                   |
              v                   v
        Continue Pipeline      Fix Code
```

## 6. Built-in GoLang Testing Framework
Go provides a built-in testing package.
```bash
package testing
```
Go testing follows these rules:
| Rule               | Description        |
| ------------------ | ------------------ |
| Test file name     | `_test.go`         |
| Test function name | `TestFunctionName` |
| Parameter          | `t *testing.T`     |

Example:
```
func TestAdd(t *testing.T)
```

---

## 7. Basic Unit Test Example

### Step 1: Application Code
File: `math.go`
```
package mathutils

func Add(a int, b int) int {
    return a + b
}
```
### Step 2: Test File
File: `math_test.go`
```
package mathutils

import "testing"

func TestAdd(t *testing.T) {
    result := Add(2,3)

    if result != 5 {
        t.Errorf("Expected 5 but got %d", result)
    }
}
```
### Step 3: Run Tests
```bash
go test ./...
```
Output:
```
PASS
ok mathutils 0.002s
```

---

## 8. GoLang Unit Testing Commands

| Command        | Description               |
| -------------- | ------------------------- |
| go test        | run tests                 |
| go test ./...  | run tests in all packages |
| go test -v     | verbose output            |
| go test -cover | code coverage             |
| go test -race  | detect race conditions    |

Example:
```bash
go test -v -cover ./...
```
---

## 9. Code Coverage
Code coverage tells how much of the code is tested.

Example:
```bash
go test -cover
```
Output:
```
coverage: 85.2% of statements
```
High coverage indicates better test reliability.

---

## 10. Tools for GoLang Unit Testing
Although Go has built-in testing support, many tools enhance testing capabilities.
| Tool       | Purpose                 |
| ---------- | ----------------------- |
| Go Testing | Built-in test framework |
| Testify    | Assertions and mocking  |
| GoMock     | Mock interfaces         |
| Ginkgo     | BDD testing framework   |
| GoConvey   | Web-based test runner   |
| Cover      | Code coverage analysis  |

---

## 11. Tool Comparison
| Tool       | Type              | Ease of Use | Features              | CI Friendly |
| ---------- | ----------------- | ----------- | --------------------- | ----------- |
| Go Testing | Built-in          | Easy        | Basic testing         | Yes         |
| Testify    | Assertion library | Easy        | Assertions & mocking  | Yes         |
| GoMock     | Mocking framework | Medium      | Mock interfaces       | Yes         |
| Ginkgo     | BDD framework     | Medium      | Behavior-driven tests | Yes         |
| GoConvey   | Testing UI        | Easy        | Web dashboard         | Partial     |

---
## 12. Advantages of Unit Testing

| # | Advantage | Description |
|---|-----------|-------------|
| 1 | Faster Development | Developers can detect and fix bugs immediately during development. |
| 2 | Easier Refactoring | Code changes can be verified quickly using existing test cases. |
| 3 | Code Documentation | Unit tests act as documentation showing how the code should behave. |
| 4 | CI Integration | Tests can run automatically in CI/CD pipelines during build processes. |
| 5 | Higher Code Quality | Encourages developers to write modular, clean, and maintainable code. |

---

## 13. Best Practices for Go Unit Testing
### 13.1 Keep Tests Simple
Tests should validate one behavior only.

### 13.2 Follow Naming Conventions
```
TestFunctionName
```
Example:
```
TestUserCreation
```
### 13.3 Use Table Driven Tests
Example:
```
func TestAdd(t *testing.T) {

tests := []struct{
a int
b int
expected int
}{
{1,2,3},
{2,3,5},
{5,5,10},
}

for _, test := range tests {
result := Add(test.a, test.b)

if result != test.expected {
t.Errorf("Expected %d got %d", test.expected, result)
}

}
}
```
### 13.4 Mock External Dependencies
Use tools like GoMock.

Example:

- Database calls

- API calls

- External services

### 13.5 Maintain High Coverage
Target coverage:
```
80% or higher
```
---

## 14. Common Mistakes
| Mistake                    | Explanation               |
| -------------------------- | ------------------------- |
| Not writing tests          | leads to unstable code    |
| Testing multiple behaviors | makes debugging difficult |
| Ignoring coverage          | reduces reliability       |
| Using real services        | slows tests               |


---

## 15. Recommendation / Conclusion
After evaluating different Go testing tools:
| Tool       | Strength               |
| ---------- | ---------------------- |
| Go Testing | Simple, built-in       |
| Testify    | Assertions and mocking |
| GoMock     | Interface mocking      |
| Ginkgo     | Advanced BDD testing   |

Recommended Approach

For most CI environments, the best combination is:
```
Go Built-in Testing + Testify
```

**Why?**
- Simple to implement

- Lightweight

- CI friendly

- Strong assertion library

- Widely used in production systems

Therefore, the recommended tool stack is:
```
Go Testing + Testify
```

---
## 16. References

| Resource | Description | Link |
|----------|-------------|------|
| Go Official Documentation | Official documentation for the Go programming language | https://go.dev/doc/ |
| Go Testing Package | Official Go package used for writing unit tests | https://pkg.go.dev/testing |
| Testify Library | Popular Go testing toolkit with assertions and mocks | https://github.com/stretchr/testify |
| GoMock | Mocking framework for testing Go applications | https://github.com/golang/mock |
| Ginkgo | Behavior-driven development (BDD) testing framework for Go | https://onsi.github.io/ginkgo/ |

---

##  17. Contact Information

| Contact Type | Details                                                             |
| ------------ | ------------------------------------------------------------------- |
| Name         | Suraj Tripathi                                                      |
| Role         | DevOps Trainee                                                      |
| Email        | [suraj.tripathi.snaatak@mygurukulam.co](mailto:suraj.tripathi.snaatak@mygurukulam.co) |
