# Software Architecture Engineering Skill

## Purpose

Use this skill when designing, reviewing, or evolving the architecture of software systems.

This skill defines universal software architecture principles for building systems that are maintainable, scalable, testable, and adaptable.

It should be combined with:

- `AGENT.md`
- `.agents/reference/architecture.md`
- `.agents/reference/business-rules.md`
- `.agents/memory/`
- `.agents/plans/`

---

# Core Principle

Architecture is the organization of a software system.

Good architecture makes software:

- Easier to understand
- Easier to maintain
- Easier to test
- Easier to extend
- Easier to deploy
- Easier to replace

Architecture should reduce long-term complexity, not increase it.

---

# Architecture Philosophy

Architecture should protect business rules from technology changes.

Technology should depend on business logic.

Business logic should never depend on frameworks.

Always ask:

```txt
If we replace the framework today...

How much business logic changes?
```

The answer should ideally be:

```txt
Almost nothing.
```

---

# Architecture Goals

Good architecture should provide:

- Separation of Concerns
- High Cohesion
- Low Coupling
- Testability
- Scalability
- Maintainability
- Replaceability
- Simplicity

---

# SOLID Principles

Every design should respect SOLID where appropriate.

## S

Single Responsibility Principle

One class should have one reason to change.

---

## O

Open / Closed Principle

Open for extension.

Closed for modification.

---

## L

Liskov Substitution Principle

Derived types should replace base types safely.

---

## I

Interface Segregation Principle

Prefer many focused interfaces over one large interface.

---

## D

Dependency Inversion Principle

Depend on abstractions.

Never depend directly on implementation.

---

# Engineering Principles

Always consider:

## DRY

Don't Repeat Yourself.

---

## KISS

Keep It Simple.

---

## YAGNI

You Aren't Gonna Need It.

Avoid building speculative features.

---

## Separation of Concerns

Each layer should have a single responsibility.

---

## Composition over Inheritance

Prefer composing behavior instead of deep inheritance trees.

---

# Clean Architecture

Recommended for most business applications.

Structure:

```txt
Presentation

↓

Application

↓

Domain

↓

Infrastructure
```

Dependency rule:

```txt
Dependencies always point inward.
```

Business rules remain independent.

---

# Layer Responsibilities

## Presentation

Responsible for:

- HTTP
- Controllers
- Routes
- Middleware
- Request parsing
- Response formatting

Never place business logic here.

---

## Application

Responsible for:

- Use cases
- Orchestration
- DTOs
- Business workflows

Coordinates domain behavior.

---

## Domain

Responsible for:

- Entities
- Value Objects
- Repository Contracts
- Domain Services
- Business Rules

Should not depend on frameworks.

---

## Infrastructure

Responsible for:

- Database
- ORM
- External APIs
- Queues
- Storage
- Email
- Payment Providers

Implementation details belong here.

---

# Dependency Rule

Dependencies point inward.

```txt
Presentation

↓

Application

↓

Domain

Infrastructure
↑
```

Domain should know nothing about:

- Express
- Next.js
- Sequelize
- PostgreSQL
- Stripe
- Paystack

---

# Feature-Based Architecture

Useful for frontend applications.

Example:

```txt
features/

auth/

wallet/

payments/

dashboard/
```

Each feature owns:

- Components
- Hooks
- Services
- Types
- Tests

---

# Layer-Based Architecture

Organize by technical layer.

Example:

```txt
controllers

services

repositories

models
```

Simple and suitable for small projects.

---

# Hexagonal Architecture

Also called:

Ports and Adapters.

Business logic communicates through interfaces.

Infrastructure plugs into ports.

Useful for:

- Large systems
- Highly testable applications
- Multiple integrations

---

# Onion Architecture

Business rules remain in the center.

Outer layers depend inward.

Very similar to Clean Architecture.

---

# MVC

Model

View

Controller

Good for:

- Small CRUD systems
- Traditional web applications

Avoid placing business logic inside controllers.

---

# Modular Monolith

Preferred starting point for most SaaS products.

Characteristics:

- One deployment
- Multiple independent modules
- Clear boundaries

Example:

```txt
Auth

Wallet

Payments

Users

Reports
```

Modules communicate through application interfaces.

---

# Microservices

Use only when justified.

Suitable when:

- Teams grow
- Scaling requirements differ
- Independent deployments are needed

Avoid premature microservices.

---

# Event-Driven Architecture

Communicate using events.

Examples:

```txt
UserRegistered

↓

SendWelcomeEmail

↓

CreateWallet

↓

NotifyAdmin
```

Useful for:

- Notifications
- Background processing
- Decoupling

---

# CQRS

Separate:

Commands

from

Queries.

Useful for:

- Complex reporting
- High-scale systems

Avoid unnecessary complexity.

---

# Repository Pattern

Repositories abstract data access.

Good:

```txt
UserRepository

WalletRepository
```

Avoid leaking ORM models into business logic.

---

# Service Layer

Services should coordinate workflows.

Avoid:

Large controllers.

Avoid:

Fat repositories.

---

# Domain Entities

Entities represent business concepts.

Example:

```txt
User

Wallet

Payment

Withdrawal
```

Entities enforce business rules.

---

# Value Objects

Use Value Objects for immutable concepts.

Examples:

```txt
Money

Email

PhoneNumber

Address
```

Prefer Value Objects when identity is unnecessary.

---

# DTOs

DTOs transport data between layers.

Never expose ORM models directly.

---

# Dependency Injection

Inject dependencies.

Avoid creating dependencies inside business logic.

Good:

```txt
CreateUserUseCase(
    userRepository
)
```

Bad:

```txt
new SequelizeUserRepository()
```

inside a use case.

---

# Error Handling

Separate:

Business Errors

Infrastructure Errors

Validation Errors

Unexpected Errors

Return meaningful domain-specific errors.

---

# Scalability

Architecture should allow growth.

Scale:

- Features
- Teams
- Traffic
- Infrastructure

without major rewrites.

---

# Maintainability

Good architecture should make change easy.

A new developer should understand:

- Structure
- Flow
- Ownership

quickly.

---

# Testability

Architecture should support:

- Unit Tests
- Integration Tests
- E2E Tests

Business logic should be testable without infrastructure.

---

# Documentation

Architecture should be documented.

Maintain:

- PRD
- Architecture docs
- ADRs
- API docs
- Sequence diagrams when useful

---

# Anti-Patterns

Avoid:

- God Objects
- Massive Controllers
- Fat Services
- Tight Coupling
- Circular Dependencies
- Business Logic in Controllers
- ORM Models as Domain Models
- Shared Global State
- Premature Microservices
- Over Engineering

---

# Architecture Decision Records (ADR)

Document major decisions.

Include:

- Context
- Decision
- Alternatives
- Consequences

Do not rely on memory alone.

---

# Architecture Review Checklist

Before approving architecture verify:

- Business rules are protected.
- Layers have clear responsibilities.
- Dependencies point inward.
- Business logic is framework independent.
- Modules are cohesive.
- Coupling is low.
- Architecture supports testing.
- Documentation is updated.
- Design remains simple.

---

# Definition of Done

Architecture work is complete only when:

- Responsibilities are clearly separated.
- Dependency direction is correct.
- Business logic is independent.
- Components are cohesive.
- Architecture supports future growth.
- Tests are easy to write.
- Documentation reflects the design.
- The solution is as simple as possible while meeting current requirements.