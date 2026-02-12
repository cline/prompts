---
description: "Guides Cline to generate comprehensive test suites alongside code — covering TDD workflows, test pyramid strategy, framework patterns, and coverage analysis."
author: "Cline Team"
version: "1.0"
category: "Development"
tags: ["testing", "tdd", "quality-assurance", "test-generation", "coverage", "ci-cd"]
globs: ["**/*.test.*", "**/*.spec.*", "**/__tests__/**", "**/tests/**", "**/*.py", "**/*.ts", "**/*.js"]
---

# Testing Strategy & Test Generation Protocol

## Objective

Guide Cline to proactively generate, maintain, and improve test suites as a first-class development activity — not an afterthought. Testing is infrastructure: once embedded into CI/CD pipelines, it becomes the backbone of project reliability.

---

## Core Directive

You **MUST** treat tests as mandatory deliverables. When generating or modifying code, you **SHOULD** generate or update corresponding tests unless the user explicitly opts out.

Before using `attempt_completion`, verify:
- [ ] New/modified code has corresponding test coverage
- [ ] Tests pass (or user has been informed of expected failures)
- [ ] Edge cases and error paths are covered

---

## 1. Test Pyramid Strategy

Follow the test pyramid to allocate effort appropriately:

```
        /  E2E  \          <- Few, slow, high-confidence
       /----------\
      / Integration \      <- Moderate, test boundaries
     /----------------\
    /    Unit Tests     \  <- Many, fast, isolated
   /____________________\
```

### Unit Tests (Foundation — 70% of tests)
- Test individual functions, methods, and classes in isolation
- Mock external dependencies (databases, APIs, file system)
- **MUST** be fast (< 100ms each)
- **MUST** be deterministic — no flaky tests

### Integration Tests (Middle — 20% of tests)
- Test interactions between modules, services, or layers
- Use real dependencies where practical (test databases, in-memory stores)
- Verify API contracts, database queries, and service boundaries

### End-to-End Tests (Top — 10% of tests)
- Test critical user journeys through the full stack
- Use sparingly — they are slow and brittle
- Focus on happy paths and critical business flows

---

## 2. Test-Driven Development (TDD) Workflow

When the user requests TDD or when building new features:

```
1. RED    -> Write a failing test that defines the desired behavior
2. GREEN  -> Write the minimum code to make the test pass
3. REFACTOR -> Clean up code while keeping tests green
4. REPEAT
```

**MUST** present each step clearly to the user. Do not skip ahead.

---

## 3. Framework-Specific Patterns

### JavaScript/TypeScript (Jest / Vitest)
```typescript
describe('UserService', () => {
  describe('createUser', () => {
    it('should create a user with valid input', async () => {
      const user = await userService.createUser({ name: 'Alice', email: 'alice@example.com' });
      expect(user.id).toBeDefined();
      expect(user.name).toBe('Alice');
    });

    it('should throw on duplicate email', async () => {
      await userService.createUser({ name: 'Alice', email: 'alice@example.com' });
      await expect(
        userService.createUser({ name: 'Bob', email: 'alice@example.com' })
      ).rejects.toThrow('Email already exists');
    });

    it('should reject invalid email format', async () => {
      await expect(
        userService.createUser({ name: 'Alice', email: 'not-an-email' })
      ).rejects.toThrow('Invalid email');
    });
  });
});
```

### Python (pytest)
```python
import pytest
from services.user_service import UserService

class TestUserService:
    def test_create_user_with_valid_input(self, user_service):
        user = user_service.create_user(name="Alice", email="alice@example.com")
        assert user.id is not None
        assert user.name == "Alice"

    def test_create_user_duplicate_email_raises(self, user_service):
        user_service.create_user(name="Alice", email="alice@example.com")
        with pytest.raises(ValueError, match="Email already exists"):
            user_service.create_user(name="Bob", email="alice@example.com")

    def test_create_user_invalid_email_raises(self, user_service):
        with pytest.raises(ValueError, match="Invalid email"):
            user_service.create_user(name="Alice", email="not-an-email")
```

### C# (xUnit)
```csharp
public class UserServiceTests
{
    [Fact]
    public async Task CreateUser_WithValidInput_ReturnsUser()
    {
        var service = new UserService(mockRepo.Object);
        var user = await service.CreateUserAsync("Alice", "alice@example.com");
        Assert.NotNull(user.Id);
        Assert.Equal("Alice", user.Name);
    }

    [Fact]
    public async Task CreateUser_DuplicateEmail_ThrowsException()
    {
        var service = new UserService(mockRepo.Object);
        await service.CreateUserAsync("Alice", "alice@example.com");
        await Assert.ThrowsAsync<DuplicateEmailException>(
            () => service.CreateUserAsync("Bob", "alice@example.com"));
    }
}
```

---

## 4. What to Test — Mandatory Coverage Areas

For every function or module, **MUST** consider:

| Category | Examples |
|----------|----------|
| **Happy path** | Valid inputs produce expected outputs |
| **Edge cases** | Empty strings, zero, null, boundary values, max-length |
| **Error handling** | Invalid inputs, network failures, timeouts, permission errors |
| **State transitions** | Before/after mutations, side effects |
| **Concurrency** | Race conditions, parallel execution (when applicable) |

---

## 5. Mocking & Test Doubles Strategy

- **MUST** mock external services (APIs, databases, file system) in unit tests
- **SHOULD** use dependency injection to make code testable
- **MUST NOT** mock the system under test — only its dependencies
- **SHOULD** prefer fakes over mocks when the dependency is complex

```
Stub  -> Returns canned data (simplest)
Mock  -> Verifies interactions (use sparingly)
Fake  -> Simplified working implementation (e.g., in-memory DB)
Spy   -> Records calls for later assertion
```

---

## 6. Test Quality Checklist

Before completing any testing task, verify:

- [ ] **Descriptive names**: Test names describe the scenario, not the implementation (`should_reject_expired_token` not `test1`)
- [ ] **Arrange-Act-Assert**: Each test follows the AAA pattern clearly
- [ ] **One assertion per concept**: Tests verify one behavior (multiple `expect` calls are fine if they verify one logical outcome)
- [ ] **No test interdependence**: Tests can run in any order
- [ ] **No hardcoded sleep/delays**: Use polling, events, or test clocks
- [ ] **Meaningful assertions**: Assert specific values, not just "no error thrown"

---

## 7. Coverage Analysis

When asked about coverage or when completing a testing task:

- **SHOULD** suggest running coverage tools (`jest --coverage`, `pytest --cov`, `dotnet test --collect:"XPlat Code Coverage"`)
- **Target**: 80%+ line coverage for business logic, 90%+ for critical paths
- **MUST NOT** chase 100% — focus on meaningful coverage, not vanity metrics
- Uncovered code **SHOULD** be flagged with rationale (e.g., "UI rendering — covered by E2E tests")

---

## 8. CI/CD Integration Guidance

When setting up or advising on CI/CD:

- Tests **MUST** run on every PR/push
- Fast unit tests run first; slow integration/E2E tests run after
- Failed tests **MUST** block merge
- Coverage reports **SHOULD** be posted as PR comments
- Flaky tests **MUST** be quarantined and fixed, not ignored

<!-- 
Enterprise Considerations:
- Team-wide configurable coverage thresholds enforced across all repositories
- Test health dashboards showing pass rates, flakiness trends, and coverage gaps
- Shared test fixture and pattern libraries distributed across teams
- Automated test quality scoring and team benchmark comparisons
-->
