# GoLang Unit Testing CI Checks Documentation

---

## 1. Introduction

In modern software development, Continuous Integration (CI) ensures that code changes are automatically built, tested, and validated before merging into the main branch.

For Go (Golang) applications, Unit Testing is a critical part of CI pipelines. It ensures:

- Code correctness
- Stability
- Regression prevention
- Safe refactoring
- Higher deployment confidence

This document provides a complete guide to implementing Unit Testing in Go as part of CI checks — from basic concepts to advanced production practices.

---

## 2. What is Unit Testing in Go?

Unit Testing is the process of testing individual functions or methods in isolation to verify that they work as expected.

In Go, unit testing is supported natively using the built-in `testing` package.

Unit tests typically:

- Test small pieces of logic
- Run automatically
- Are fast
- Do not depend on external systems (DB, network)

---

## 3. Why Unit Testing in CI?

Without CI-based testing:

- Bugs reach production
- Refactoring becomes risky
- Code quality degrades
- Team confidence reduces

With CI Unit Testing:

- Every push runs tests automatically
- Merge is blocked if tests fail
- Code coverage can be enforced
- Quality gates can be applied

CI ensures that no broken code is merged.

---

## 4. Unit Testing Workflow in CI

```
Developer Push Code
        ↓
CI Triggered
        ↓
Install Dependencies
        ↓
Run go test
        ↓
Generate Coverage Report
        ↓
Pass → Merge Allowed
Fail → Merge Blocked
```

---

## 5. Basic Go Unit Test Example

### Step 1: Create Project

```bash
mkdir go-unit-demo
cd go-unit-demo
go mod init go-unit-demo
```

---

### Step 2: Create Business Logic

Create file: `math.go`

```go
package main

func Add(a int, b int) int {
	return a + b
}

func Divide(a int, b int) int {
	if b == 0 {
		return 0
	}
	return a / b
}
```

---

### Step 3: Create Unit Test File

File name must end with `_test.go`

Create: `math_test.go`

```go
package main

import "testing"

func TestAdd(t *testing.T) {
	result := Add(2, 3)
	expected := 5

	if result != expected {
		t.Errorf("Expected %d but got %d", expected, result)
	}
}

func TestDivide(t *testing.T) {
	result := Divide(10, 2)
	expected := 5

	if result != expected {
		t.Errorf("Expected %d but got %d", expected, result)
	}
}
```

---

### Step 4: Run Tests Locally

```bash
go test ./...
```

Run with coverage:

```bash
go test -cover ./...
```

---

## 6. CI Integration Example (GitHub Actions)

Create file:

`.github/workflows/go-ci.yml`

```yaml
name: Go CI

on:
  push:
    branches: [ "main" ]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup Go
        uses: actions/setup-go@v4
        with:
          go-version: '1.22'

      - name: Install Dependencies
        run: go mod tidy

      - name: Run Tests
        run: go test -v -cover ./...
```

Now every push triggers automatic unit testing.

---

## 7. Advanced Testing Concepts

### 7.1 Table Driven Tests

```go
func TestAddTableDriven(t *testing.T) {
	tests := []struct {
		a, b     int
		expected int
	}{
		{2, 3, 5},
		{5, 5, 10},
		{0, 1, 1},
	}

	for _, test := range tests {
		result := Add(test.a, test.b)
		if result != test.expected {
			t.Errorf("Expected %d but got %d",
				test.expected, result)
		}
	}
}
```

---

### 7.2 Mocking in Go

Go does not have built-in mocking, but tools like:

- GoMock
- Testify

are commonly used.

---

## 8. Popular Go Testing Tools

| Tool | Purpose | Type |
|------|----------|------|
| testing | Built-in unit testing | Standard |
| Testify | Assertions & mocking | Third-party |
| GoMock | Advanced mocking | Third-party |
| Ginkgo | BDD testing framework | Third-party |
| GoConvey | Web UI based testing | Third-party |

---

## 9. Tool Comparison

| Feature | testing | Testify | GoMock | Ginkgo |
|----------|---------|----------|---------|---------|
| Built-in | Yes | No | No | No |
| Assertions | Basic | Advanced | No | Yes |
| Mocking | No | Yes | Yes | Yes |
| BDD Style | No | No | No | Yes |
| Learning Curve | Low | Low | Medium | Medium |

---

## 10. Advantages of Unit Testing in CI

- Early bug detection
- Faster debugging
- Safer deployments
- Improved developer confidence
- Enforced code coverage
- Supports DevOps practices

---

## 11. Proof of Concept (POC)

POC Objective:

- Create a small Go app
- Write unit tests
- Integrate into CI
- Ensure pipeline fails on test failure

Steps:

1. Create Go module
2. Write business logic
3. Write unit test
4. Configure GitHub Actions
5. Push code
6. Verify CI pipeline status

Expected Result:

- Tests pass → CI Success
- Tests fail → CI Failure

---

## 12. Best Practices

1. Keep tests independent
2. Use table-driven tests
3. Aim for at least 70–80% coverage
4. Avoid external dependencies in unit tests
5. Use mocking for DB/API
6. Run tests in every PR
7. Keep tests fast
8. Separate unit and integration tests

---

## 13. Code Coverage Enforcement (Advanced)

You can fail CI if coverage is below threshold:

```bash
go test -coverprofile=coverage.out ./...
go tool cover -func=coverage.out
```

Custom script can check minimum coverage percentage.

---

## 14. Recommended CI Pipeline Structure

Stage 1: Lint  
Stage 2: Unit Test  
Stage 3: Coverage Check  
Stage 4: Build  
Stage 5: Docker Build (Optional)  

Unit testing must run before build artifacts are created.

---

## 15. Conclusion & Recommendation

For GoLang CI Unit Testing:

Primary Choice: Built-in `testing` package  
Enhancement Tool: `Testify`

Reason:

- `testing` is lightweight and native
- No external dependency required
- Fast execution
- Easy CI integration
- Production proven

For enterprise-grade projects:

Recommended Stack:

testing + Testify

I recommend starting with:

**testing (built-in) as foundation**
Then add:
**Testify for assertions and mocking**

This gives simplicity + power + maintainability.

---

## 16. Contact Information

Author: Suraj Tripathi  
Project: GoLang CI Unit Testing Guide  
Environment: Production-ready CI/CD setup  

---

## 17. References

- https://go.dev/doc/tutorial/add-a-test
- https://pkg.go.dev/testing
- https://github.com/stretchr/testify
- https://github.com/golang/mock
- https://docs.github.com/actions

---

END OF DOCUMENT
