# .NET Solution Structure & Clean Architecture

## Purpose

This document defines the **authoritative .NET solution structure**
and **Clean Architecture layering** for the Enterprise Architecture Visibility &
Intelligence Platform (EAVIP).

It ensures:
- Clear separation of concerns
- Testability and maintainability
- Replaceable infrastructure (DBs, queues, search)
- Governance and security enforced at the right layers

This is the **engineering structure contract** for all .NET development.

---

## Architectural Principles (Locked)

1. Domain is independent of frameworks
2. Dependencies point inward
3. Infrastructure is replaceable
4. Commands mutate state; queries never do
5. No business logic in controllers
6. Cross-cutting concerns via middleware/pipelines

---

## Solution Layout (Authoritative)
/src
/Eavip.Domain
/Eavip.Application
/Eavip.Infrastructure
/Eavip.Api
/Eavip.Workers
/tests
/Eavip.Domain.Tests
/Eavip.Application.Tests
/Eavip.Infrastructure.Tests
/Eavip.Api.Tests


Each project has a **single, strict responsibility**.

---

## 1. Eavip.Domain (Pure Core)

### Responsibility
- Business rules
- Domain models
- Invariants
- Value objects

### Contains
- Entities (Enterprise, Org, App, Component, Dependency)
- Value Objects (ConfidenceScore, TimeRange, Ownership)
- Domain Services (pure logic)
- Domain Events (intent-level)

### Rules
- ❌ No EF Core
- ❌ No Neo4j driver
- ❌ No logging
- ❌ No framework dependencies

This project must compile with **zero infrastructure references**.

---

## 2. Eavip.Application (Use Cases)

### Responsibility
- Orchestrate domain behavior
- Enforce application-level rules
- Authorization & validation

### Contains
- Commands & Command Handlers
- Queries & Query Handlers
- DTOs
- Interfaces (IGraphRepository, IEventBus, ISearchIndex)
- Application policies

### Rules
- Depends on Domain
- Does NOT depend on Infrastructure
- No persistence details
- No HTTP concerns

This layer defines **what the system does**.

---

## 3. Eavip.Infrastructure (Adapters)

### Responsibility
- Implement external concerns
- Translate interfaces into concrete tech

### Contains
- Neo4j repositories
- EF Core DbContexts
- OpenSearch clients
- Messaging adapters (Kafka, RabbitMQ, etc.)
- File/object storage adapters
- Auth providers (OIDC integration)

### Rules
- Depends on Application + Domain
- No business rules
- Replaceable implementations

Infrastructure can be swapped without touching Domain/Application.

---

## 4. Eavip.Api (Delivery Mechanism)

### Responsibility
- HTTP API exposure
- AuthN/AuthZ enforcement
- Request validation
- Response shaping

### Contains
- Controllers (thin)
- Middleware (auth, tenant, correlation)
- API filters
- OpenAPI configuration

### Rules
- No business logic
- Calls Application layer only
- Handles transport concerns

---

## 5. Eavip.Workers (Background Processing)

### Responsibility
- Async processing
- Event handling
- Long-running tasks

### Contains
- Event consumers
- Projection builders
- Indexing jobs
- Webhook dispatchers

### Rules
- Uses Application layer
- No direct Domain mutation
- Idempotent processing required

---

## Dependency Rule (Non-Negotiable)
Api → Application → Domain
Workers → Application → Domain
Infrastructure → Application → Domain


No reverse dependencies allowed.

---

## Cross-Cutting Concerns

Handled via:
- ASP.NET Core middleware
- MediatR pipelines (or equivalent)
- Filters and decorators

Examples:
- Authorization
- Validation
- Logging
- Correlation IDs
- Transactions

---

## CQRS Pattern (Enforced)

### Commands
- Mutate state
- Go through governance
- Emit domain events

### Queries
- Read-only
- Optimized for views
- No side effects

Commands and queries never share handlers.

---

## Testing Strategy

### Domain Tests
- Pure unit tests
- No mocks for logic

### Application Tests
- Mock infrastructure interfaces
- Validate workflows and rules

### Infrastructure Tests
- Integration tests
- Real Neo4j / PostgreSQL / OpenSearch

### API Tests
- Contract tests
- Auth and permission checks

---

## What This Structure Avoids

- Fat controllers
- Anemic domain models
- Infrastructure leakage
- Tight coupling
- Untestable code

---

## Outcome

With this structure:
- Codebase scales cleanly
- On-Prem and Cloud share code
- Refactoring is safe
- New engineers onboard quickly
- Architecture intent remains enforceable

---

## Status

This document defines the **authoritative .NET solution structure and Clean Architecture model**.
All .NET implementation must conform to this structure.


