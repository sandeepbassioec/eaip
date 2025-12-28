# EAVIP – Architecture Laws & Coding Standards
*(Non-Negotiable / Architecture Constitution)*

---

## 1. Purpose of This Document

This document defines the **absolute architectural laws** governing the
design and implementation of the **Enterprise Architecture Visibility &
Intelligence Platform (EAVIP)**.

It exists to:

- Prevent architectural drift during implementation
- Eliminate accidental complexity
- Enforce enterprise-grade engineering discipline
- Align execution with TOGAF + DDD principles
- Ensure the codebase remains understandable, evolvable, and scalable
  even with **100,000+ classes**

These laws override:
- Individual coding preferences
- Framework defaults
- Convenience-driven shortcuts

---

## 2. Core Architectural Philosophy

### 2.1 Architecture-First Execution

- Architecture is finalized **before** code
- Code is a *consequence* of architecture, not the driver
- No implementation detail may introduce a new architectural decision

### 2.2 Explainability Over Cleverness

- Every design must be explainable to:
  - Architects
  - Senior engineers
  - Future maintainers (5–10 years later)
- Implicit behavior is forbidden
- Magic is treated as technical debt

---

## 3. Layering Laws (Strict)

EAVIP follows a **strict layered architecture**.
Domain
Application
Infrastructure
API

### 3.1 Dependency Rule (Non-Negotiable)

Dependencies may flow **only downward**:
API → Application → Domain
Infrastructure → Application → Domain

Forbidden:
- Domain depending on Application
- Domain depending on Infrastructure
- Domain depending on frameworks
- Application depending on Infrastructure implementations

---

## 4. Domain Layer Laws (DDD Purity)

### 4.1 What the Domain Layer IS

The Domain Layer represents **business truth**, nothing else.

It contains:
- Aggregates
- Entities
- Value Objects
- Domain Events
- Domain Invariants

### 4.2 What the Domain Layer MUST NOT Contain

The following are **STRICTLY FORBIDDEN** in Domain:

- Repository interfaces
- Unit of Work
- MediatR
- Policies
- Validation pipelines
- EF Core attributes
- JSON attributes
- Logging
- Configuration
- Tenant resolution
- Infrastructure concerns
- Conditional orchestration logic

If any of the above appear in Domain → **architecture violation**

---

## 5. Aggregate & Aggregate Root Laws

### 5.1 Aggregate Definition

An Aggregate is:
- A transactional consistency boundary
- A cluster of entities treated as a single unit

### 5.2 Aggregate Root Rules

- Exactly **one Aggregate Root** per aggregate
- All external access goes through the root
- No external object may hold references to internal entities
- Cross-aggregate references are by **ID only**

### 5.3 Mutation Rules

- All state changes must:
  - Be initiated via Aggregate Root methods
  - Enforce invariants
  - Emit Domain Events when something meaningful changes

---

## 6. Application Layer Laws (Use-Case Orchestration)

### 6.1 Responsibility

The Application Layer:
- Orchestrates use cases
- Coordinates domain objects
- Applies policies
- Manages transactional boundaries

It does **NOT** contain business truth.

### 6.2 Allowed Constructs

- Commands & Queries
- Command / Query Handlers
- Policy pipelines
- Repository abstractions
- Unit of Work
- Domain Event dispatch coordination

### 6.3 Repository Law (Critical)

- `IRepository<T>` is a **generic, cross-domain abstraction**
- Repositories belong to the **Application layer**
- No domain-specific repository interfaces are allowed

Correct:
IRepository<Enterprise>
IRepository<Application>

Incorrect:
IEnterpriseRepository
IApplicationRepository

---

## 7. Infrastructure Layer Laws

### 7.1 Responsibility

Infrastructure is responsible for:
- Persistence (EF Core, SQL, Neo4j)
- Messaging (Outbox, Kafka, RabbitMQ)
- Caching
- File systems
- External service integrations

### 7.2 Conditional Logic Rule

- Infrastructure **may** use `if`, `switch`, retries, fallbacks
- This logic must be:
  - Deeply encapsulated
  - Invisible to Domain and Application layers

Infrastructure absorbs complexity so the domain remains pure.

---

## 8. API Layer Laws (Transport Only)

### 8.1 Responsibility

The API layer is a **transport adapter**, nothing more.

It may:
- Translate HTTP → Command / Query
- Handle authentication
- Handle authorization
- Handle serialization

It must NOT:
- Contain business logic
- Perform orchestration
- Contain domain rules

---

## 9. Conditional Logic & Expression-Based Design (Locked)

### 9.1 High-Level Rule

- Business logic must be:
  - Expression-based
  - Policy-driven
  - Pipeline-oriented

### 9.2 Forbidden in Business Logic

- `if / else`
- `switch`
- nested conditionals
- hard-coded rule branching

### 9.3 Allowed Alternatives

- Specification pattern
- Policy objects
- Expression trees
- Predicate composition
- Rule engines (internal, deterministic)

Infrastructure-level null checks are allowed but minimized.

---

## 10. Multi-Tenancy Law

### 10.1 Principle

Multi-tenancy is:
- A **cross-cutting infrastructure concern**
- NOT a domain concern

### 10.2 Rules

- Domain entities do NOT carry TenantId
- Tenant isolation is enforced:
  - At repository implementation level
  - Via query filters
  - Via connection scoping

The domain remains tenant-agnostic by design.

---

## 11. Technology Neutrality Law

### 11.1 Platform Stance

EAVIP is:
- Cloud-neutral
- Database-neutral
- Messaging-neutral

### 11.2 Reference Implementations

For implementation and learning purposes:
- Backend: .NET (C#)
- Frontend: React + TypeScript
- Databases: PostgreSQL, SQL Server

These are **reference choices**, not hard dependencies.

---

## 12. No Duplication Law

- No architectural concept may be redefined per domain
- Cross-cutting abstractions exist exactly once
- Horizontal concerns are centralized

Violation indicator:
> “We’ll duplicate this for now and refactor later”

This is forbidden.

---

## 13. Evolution & Safety Law

- Architecture must allow:
  - New domains without refactoring old ones
  - New storage engines without touching domain
  - New delivery models without rewriting logic

If a design blocks future domains → reject it.

---

## 14. Enforcement

- Any violation of these laws is a **hard stop**
- Architecture correctness > delivery speed
- Refactoring is allowed only if architecture improves

---

## 15. Final Statement

This document is the **constitution of EAVIP**.

All future:
- Code
- Design
- Reviews
- Refactors

Must comply with these laws.
