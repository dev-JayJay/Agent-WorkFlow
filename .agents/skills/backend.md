# Backend Engineering Skill

## Purpose

This document defines the universal backend engineering principles used across all projects.

It is framework-agnostic and reusable.

These principles should be followed unless project-specific documentation (`AGENT.md`, `reference/`, or `memory/`) explicitly overrides them.

This skill represents the preferred engineering philosophy for designing scalable, maintainable, and production-ready backend systems.

---

# Engineering Philosophy

The backend exists to enforce business rules.

Frameworks, databases, HTTP servers, and third-party services are implementation details.

Business logic should survive changes to technology.

Always optimize for:

* Maintainability
* Testability
* Simplicity
* Separation of Concerns
* Explicitness over Magic
* Composition over Inheritance

---

# Architectural Style

Unless the project specifies otherwise, backend systems should follow Clean Architecture.

```
src/

├── domain/
│   ├── entities/
│   ├── repositories/
│   └── errors/
│
├── application/
│   ├── use-cases/
│   ├── dto/
│   └── interfaces/
│
├── infrastructure/
│   ├── database/
│   │   ├── sequelize/
│   │   └── config.ts
│   │
│   ├── repositories/
│   └── services/
│
├── presentation/
│   ├── controllers/
│   ├── routes/
│   └── middlewares/
│
├── shared/
│   ├── utils/
│   ├── constants/
│   └── types/
│
└── server.ts
```

---

# Layer Responsibilities

## Domain

Contains pure business logic.

Responsibilities:

* Entities
* Value Objects
* Repository Contracts
* Domain Errors

The Domain must never know:

* Express
* Fastify
* Sequelize
* Prisma
* PostgreSQL
* HTTP
* JWT
* REST

The Domain should be portable.

---

## Application

Coordinates business operations.

Contains:

* Use Cases
* DTOs
* Interfaces
* Business workflows

Application may depend on:

* Domain
* Shared

Application must not depend on infrastructure implementations.

---

## Infrastructure

Implements external systems.

Examples:

* Database
* ORM
* Redis
* Email
* Payment Providers
* Cloud Storage
* Repository Implementations

Infrastructure can depend on:

* Domain
* Application
* Shared

---

## Presentation

Responsible only for communication.

Contains:

* Controllers
* Routes
* Middleware
* HTTP Mapping

Controllers should:

* Parse requests
* Validate input
* Call use cases
* Return responses

Controllers should never contain business logic.

---

## Shared

Contains reusable utilities.

Examples:

* Logger
* Constants
* Types
* Helpers
* Result wrappers

Avoid placing business logic here.

---

# Dependency Rule

Dependencies always point inward.

```
Presentation
      ↓

Application
      ↓

Domain

Infrastructure
      ↓

Application
      ↓

Domain
```

Never import framework-specific code into the Domain.

---

# Entity Rules

Entities represent business concepts.

Entities should:

* Contain behavior
* Protect invariants
* Be framework independent
* Be immutable where practical

Entities should not:

* Query databases
* Read HTTP requests
* Know about APIs

---

# Repository Rules

Repositories abstract persistence.

Repositories define WHAT is needed.

Infrastructure decides HOW.

Good:

```
findById()

findByEmail()

save()

delete()
```

Avoid ORM-specific methods leaking into business logic.

---

# Use Case Rules

Each use case should solve one business problem.

Examples:

```
CreateUserUseCase

PurchaseQuizUseCase

WithdrawFundsUseCase
```

Avoid giant services.

Keep use cases cohesive.

---

# Controller Rules

Controllers should remain thin.

Typical flow:

```
Request

↓

Validate

↓

Use Case

↓

Response
```

Never perform business calculations inside controllers.

---

# Validation Rules

Validate all external input.

Examples:

* Body
* Query
* Params
* Environment Variables
* Webhooks

Fail fast.

Return consistent validation errors.

---

# Error Handling

Use explicit error types.

Examples:

* ValidationError
* UnauthorizedError
* ForbiddenError
* ConflictError
* NotFoundError

Never expose internal stack traces.

---

# Transactions

Use transactions whenever multiple state changes must succeed together.

Examples:

* Payments
* Wallets
* Orders
* Inventory
* Transfers

---

# Idempotency

Protect retryable operations.

Examples:

* Webhooks
* Payment callbacks
* Queue jobs

Prefer:

* Unique event IDs
* Database constraints
* Processed-event tables

---

# Security Principles

Always enforce:

* Authentication
* Authorization
* Ownership
* Validation

Never trust frontend validation.

Never log secrets.

---

# API Design

Prefer RESTful APIs.

Use consistent response formats.

Support pagination where appropriate.

Keep endpoints resource-oriented.

---

# Testing Strategy

Every backend feature should include:

* Unit Tests
* Integration Tests
* Edge Cases

Business rules should always be unit tested.

---

# Naming Conventions

Entities

```
User.ts
Wallet.ts
Order.ts
```

Repositories

```
IUserRepository.ts
```

Use Cases

```
CreateUserUseCase.ts
```

Controllers

```
UserController.ts
```

DTOs

```
CreateUserDto.ts
```

---

# Code Quality Principles

Always prefer:

* Small functions
* Single Responsibility
* Explicit naming
* Reuse existing patterns
* Readability over cleverness

Avoid:

* Massive services
* Deep nesting
* Duplicate logic
* Hidden side effects
* Premature optimization

---

# Definition of Done

Backend work is complete only when:

* Business rules are implemented.
* Validation exists.
* Authorization exists.
* Tests pass.
* Existing architecture is respected.
* Documentation is updated if needed.
* The implementation matches project conventions.
