# Testing Engineering Skill

## Purpose

Use this skill when designing, implementing, reviewing, or improving tests.

This skill defines reusable testing principles for building reliable software with confidence.

It should be combined with project-specific context from:

- `AGENT.md`
- `.agents/reference/`
- `.agents/memory/`
- `.agents/plans/`
- Existing test files and test setup

---

# Core Principle

Testing is not just about proving that code works.

Testing is about creating confidence that the system behaves correctly under normal, edge, and failure conditions.

Good tests should be:

- Clear
- Repeatable
- Fast enough
- Focused
- Maintainable
- Business-rule aware

---

# Testing Philosophy

Test behavior, not implementation details.

Prefer tests that answer:

```txt
Given this situation,
when this action happens,
then this result should occur.

```

Avoid testing implementation details.

Tests should remain valid even if internal implementation changes.

---

# Testing Pyramid

Build confidence using the Testing Pyramid.

```txt
           E2E
          /   \
     Integration
     /         \
   Unit Tests
```

Prioritize:

- Many Unit Tests
- Some Integration Tests
- Few End-to-End Tests

---

# Unit Testing

Unit tests verify a single unit of behavior.

Good candidates:

- Services
- Use Cases
- Domain Entities
- Utility Functions
- Validators
- Business Rules

Unit tests should:

- Be fast.
- Run independently.
- Avoid databases.
- Avoid external APIs.
- Avoid filesystem access.
- Use mocks, stubs, fakes, or spies when needed.

Examples:

```txt
CreateUserUseCase

PurchaseQuizUseCase

CalculateScore()

ValidateExamImport()
```

---

# Integration Testing

Integration tests verify multiple components working together.

Good candidates:

- API + Database
- Repository + Database
- Controller + Service
- Authentication
- Authorization
- Payment workflows
- Webhooks
- Import pipelines

Integration tests should use:

- Test databases
- Docker containers
- Temporary storage
- Local infrastructure

Avoid mocking everything.

---

# End-to-End Testing

E2E tests simulate real user behavior.

Examples:

```txt
Register

↓

Login

↓

Deposit Wallet

↓

Purchase Quiz

↓

Start Quiz

↓

Submit Quiz

↓

View Result
```

Only test high-value user journeys.

Keep E2E tests minimal but meaningful.

---

# Arrange Act Assert

Structure every test using AAA.

```txt
Arrange

↓

Act

↓

Assert
```

Example:

```ts
it("should reject duplicate purchases", async () => {
  // Arrange

  // Act

  // Assert
});
```

---

# Given When Then

Business tests should read like specifications.

Example:

```txt
Given

User owns quiz

When

User purchases again

Then

Purchase should be rejected
```

---

# Test Naming

Names should describe behavior.

Good:

```txt
should reject duplicate payment reference
```

Good:

```txt
should create wallet after successful registration
```

Avoid:

```txt
test payment
```

---

# Test Doubles

Choose the correct test double.

## Mock

Verify interactions.

Example:

```txt
Email service called.
```

---

## Stub

Return predefined responses.

Example:

```txt
Payment gateway returns success.
```

---

## Fake

Lightweight working implementation.

Example:

```txt
InMemoryUserRepository
```

---

## Spy

Observe behavior.

Example:

```txt
AuditLogger recorded action.
```

---

# API Testing

Every endpoint should test:

- Success
- Validation failure
- Authentication
- Authorization
- Resource not found
- Duplicate request
- Invalid state
- Unexpected server error

Validate:

- Status codes
- Response body
- Error messages
- Side effects
- Database changes

---

# Business Rule Testing

Business rules deserve the highest confidence.

Examples:

Wallet

```txt
Cannot go negative.
```

Purchase

```txt
Cannot purchase twice.
```

Withdrawal

```txt
Minimum withdrawal enforced.
```

Booking

```txt
Cannot reserve unavailable slot.
```

Business rules should have multiple positive and negative tests.

---

# Database Testing

Verify:

- Migrations
- Relationships
- Constraints
- Transactions
- Rollbacks
- Repository methods
- Soft deletes
- Unique constraints

Use integration tests.

---

# Transaction Testing

Test every transaction for:

- Success
- Rollback
- Partial failure
- Concurrent execution

Never assume transactions work.

Verify them.

---

# Money Flow Testing

Financial features require extra attention.

Test:

- Wallet credit
- Wallet debit
- Double spending
- Duplicate webhook
- Failed transfer
- Successful transfer
- Ledger consistency
- Balance calculations

Every financial operation should leave consistent data.

---

# Webhook Testing

Verify:

- Valid signature
- Invalid signature
- Duplicate webhook
- Unknown event
- Missing reference
- Retry behavior
- Idempotency

Never trust provider callbacks blindly.

---

# Authentication Testing

Verify:

- Login success
- Login failure
- Expired token
- Invalid token
- Missing token
- Refresh flow
- Logout

---

# Authorization Testing

Verify:

- Owner access
- Admin access
- Normal user restrictions
- Role permissions
- Resource ownership

Example:

```txt
User A

↓

Cannot update

↓

User B's profile
```

---

# Security Testing

Test:

- SQL Injection
- XSS
- CSRF (where applicable)
- Rate limiting
- Input validation
- Permission escalation
- Secret exposure
- Sensitive endpoints

---

# Frontend Testing

Test behavior instead of implementation.

Examples:

- Form validation
- Button actions
- Error messages
- Loading states
- Empty states
- Navigation
- Dialogs
- Drawers
- Accessibility

Use semantic queries where possible.

---

# Performance Testing

Performance should be measured.

Consider:

- Load Testing
- Stress Testing
- Spike Testing
- Soak Testing

Measure:

- Response time
- Throughput
- Resource usage

---

# Edge Cases

Always consider:

- Empty input
- Null values
- Invalid types
- Boundary values
- Duplicate requests
- Network failures
- Timeouts
- Expired resources
- Concurrent requests

---

# Regression Testing

Every bug fixed should receive a regression test.

The bug should never return unnoticed.

---

# Test Data

Use factories/builders.

Example:

```txt
createUser()

createWallet()

createPayment()

createQuiz()
```

Avoid huge inline objects.

---

# Test Isolation

Tests should never depend on one another.

Rules:

- Independent execution
- Clean database
- Clear mocks
- Reset shared state

---

# Continuous Integration

CI should automatically run:

```bash
lint

↓

typecheck

↓

unit tests

↓

integration tests

↓

build
```

Failed validation should block merges.

---

# Code Coverage

Coverage is a guide, not the goal.

Aim for:

- High coverage of business logic.
- Meaningful assertions.
- Strong edge-case testing.

Avoid writing tests only to increase percentage.

---

# Review Checklist

Before approving test work verify:

- Business rules are covered.
- Success paths are tested.
- Failure paths are tested.
- Edge cases are tested.
- Security scenarios are covered.
- Critical workflows are tested.
- Test names are readable.
- Tests are deterministic.
- Tests pass consistently.

---

# Common Anti-Patterns

Avoid:

- Testing private methods.
- Sleeping in tests.
- Shared mutable state.
- Random test order.
- Excessive mocking.
- Ignoring edge cases.
- Large monolithic tests.
- Testing framework internals.

---

# Definition of Done

Testing work is complete only when:

- Business rules are verified.
- Critical user journeys are covered.
- Unit tests pass.
- Integration tests pass.
- E2E tests pass where applicable.
- CI passes.
- Regression tests exist for fixed bugs.
- Tests are readable and maintainable.
- The implementation inspires confidence.