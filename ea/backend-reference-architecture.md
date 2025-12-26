# Backend Reference Architecture – Skeleton Implementation
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines the **backend reference architecture** for implementing
the Walking Skeleton of EAVIP.

It translates:
- TOGAF execution intent
- DDD bounded contexts
- Modular Monolith strategy

into **concrete backend code structure**, patterns, and rules.

This is the **gold standard** that all future backend development must follow.

---

## Core Principle (Locked)

**Architecture is enforced by code structure, not conventions.**

If structure allows violations, violations will happen.

---

## Technology Stack (Locked for Phase-1)

- Language: **C#**
- Runtime: **.NET 8**
- API: **ASP.NET Core**
- ORM (Write): **EF Core**
- Query (Read): **Dapper**
- Messaging (Internal): **In-memory domain events**
- External Messaging (Future): **Kafka / RabbitMQ via adapters**
- Auth: **JWT / OAuth2 (extensible)**
- Validation: **FluentValidation**
- Testing: **xUnit + FluentAssertions**

---

## Solution Structure

/src
/EAVIP.Architecture.Core
/Domain
/Application
/Infrastructure
/API

/EAVIP.SharedKernel

/EAVIP.Host


---

## Project Responsibilities

### EAVIP.Architecture.Core

Owns:
- Enterprise
- Organization
- Application
- Component
- Dependency
- DataFlow

This project is **authoritative** for core architecture data.

---

### EAVIP.SharedKernel (Minimal)

Contains:
- Strongly-typed IDs
- Time abstractions
- Base domain interfaces

Must NEVER contain:
- Entities
- Aggregates
- Repositories
- Business logic

---

### EAVIP.Host

- ASP.NET Core startup
- Dependency Injection
- Middleware
- Cross-cutting concerns
- Hosting configuration

No domain logic allowed.

---

## Domain Layer Design

### Aggregate Root Example: `Application`

Responsibilities:
- Enforce invariants
- Manage lifecycle
- Emit domain events

Rules:
- Constructor is private
- Creation via static factory
- State changes via methods
- Events raised internally

No persistence concerns here.

---

## Application Layer Design

### Commands

- One command = one intent
- Example: `CreateApplication`

### Command Handlers

Responsibilities:
- Load required aggregates
- Invoke aggregate methods
- Persist changes
- Dispatch domain events

Must NOT:
- Contain business rules
- Mutate state directly

---

## Persistence Strategy

### Write Model (EF Core)

- One DbContext per bounded context
- DbContext lives in Infrastructure
- Repositories wrap DbContext
- No DbContext leaks upward

### Read Model (Dapper)

- Separate query models
- Optimized for reads
- No tracking
- No domain objects returned

---

## Domain Events Handling

- Events raised in Domain
- Collected during transaction
- Dispatched after commit
- Handlers live in Application layer

Future externalization is seamless.

---

## API Layer Design

### Controllers

Responsibilities:
- Accept requests
- Validate input
- Map to commands
- Return responses

Controllers are **thin by design**.

---

## Dependency Rules (Enforced)

Allowed:
- API → Application
- Application → Domain
- Infrastructure → Application + Domain

Forbidden:
- Domain → Application
- Domain → Infrastructure
- API → Domain

---

## Transaction Boundaries

- One command = one transaction
- Aggregate consistency guaranteed
- Cross-aggregate consistency via events

No distributed transactions.

---

## Error Handling Strategy

- Domain exceptions for business violations
- Application exceptions for orchestration issues
- API maps exceptions to HTTP responses

No leaking internals.

---

## Testing Strategy

### Unit Tests
- Aggregates
- Domain services
- Invariants

### Integration Tests
- Command handlers
- Persistence
- Event handling

### Architecture Tests
- Dependency rules
- Forbidden references

---

## Trade-offs (Explicit)

### Pros
- Strong domain integrity
- Clear separation
- Easy testing
- Evolvable architecture

### Cons
- More files
- Learning curve
- Discipline required

Accepted deliberately.

---

## Why This Architecture Works

- Enforces DDD principles
- Maps directly from TOGAF execution
- Scales with complexity
- Prevents architectural erosion

This backend can scale to **hundreds of thousands of classes** safely.

---

## Next Step

Proceed to **Frontend Reference Architecture**

File: `ea/frontend-reference-architecture.md`
