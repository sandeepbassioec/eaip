# Repository Pattern & Unit of Work (DDD Execution Guide)
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document explains **how repositories and persistence are implemented**
in a DDD + CQRS system like EAVIP **without falling into ORM-driven design**.

It answers:
- What exactly a repository should do (and not do)
- How aggregates are persisted safely
- How Unit of Work fits in modern .NET systems
- How to use EF Core / Dapper correctly
- How to avoid “anemic domain + fat handlers”

This document is execution-focused and intended as a long-term reference.

---

## Core Rule (Locked)

**Repositories exist for Aggregate Roots only — never for entities or tables.**

Violating this rule collapses DDD into CRUD-based chaos.

---

## What a Repository Really Is

A repository is:
- A collection-like abstraction
- Responsible for Aggregate Roots
- A boundary between domain and persistence

A repository is NOT:
- A query service
- A DAO
- A DbContext wrapper
- A place for business logic

---

## Repository Responsibilities (Strict)

A repository MUST:
1. Load an aggregate root by its identity
2. Persist the aggregate root
3. Enforce aggregate boundaries
4. Hide storage and ORM details

A repository MUST NOT:
- Return child entities directly
- Expose IQueryable
- Join across aggregates
- Contain business rules

---

## Example: Application Aggregate Repository

### Aggregate Root
`Application`

### Repository Interface (Conceptual)

- GetById(ApplicationId)
- Save(Application)

If a repository has many finder methods, it is incorrectly designed.

---

## Where Queries Belong

Queries **do not belong in repositories**.

| Concern | Correct Location |
|------|------------------|
| Commands | Aggregates + Repositories |
| Queries | Query Handlers / Read Models |
| Reports | Reporting Service |
| Search | Search Index |
| Joins | Read-side projections |

Repositories are **write-side only**.

---

## Unit of Work (Modern Interpretation)

### Traditional View
- Explicit UnitOfWork classes
- Manual transaction control

### Modern .NET Reality
- DbContext already acts as Unit of Work
- One command = one transaction

**Locked Rule**  
One command execution represents one unit of work.

If multiple aggregates must be updated together, the design is wrong.

---

## Correct Command Execution Flow

1. Controller receives request
2. CommandHandler executes
3. Repository loads aggregate root
4. Aggregate enforces business rules
5. Repository saves aggregate
6. Transaction commits
7. Domain events are persisted to outbox

Handlers orchestrate.  
Aggregates decide.

---

## Domain Events & Persistence

Repositories do not publish events directly.

Correct pattern:
- Aggregate raises domain events
- Repository persists aggregate and events
- Outbox dispatcher publishes events asynchronously

This guarantees consistency and reliability.

---

## EF Core Usage (Safe Pattern)

EF Core is used for:
- Persistence mapping
- Change tracking
- Transaction management

EF Core is NOT used for:
- Business logic
- Cross-aggregate joins
- Query optimization

### Mapping Rules
- Aggregate Root is the EF root
- Child entities are private collections
- No navigation properties to other aggregates

---

## Read Side: Dapper / SQL / Projections

Read-side queries:
- Ignore aggregate purity
- Optimize for performance
- Use denormalized structures

Valid tools:
- Dapper
- Raw SQL
- EF Core projections
- OpenSearch

Read models are disposable and rebuildable.

---

## Snapshot / Projection Models

A snapshot is a **denormalized read model**, for example:
- ApplicationId
- ApplicationName
- CountryName
- RiskScore
- CostScore

Snapshots exist to:
- Serve UI needs
- Avoid aggregate pollution
- Improve query performance

Historical accuracy is preferred over cosmetic freshness.

---

## Handling UI Scenarios (Country Name Example)

Correct pattern:
- Command saves aggregate with CountryId
- UI calls query endpoint
- Query returns CountryName via projection

Never load or reference another aggregate inside an aggregate.

---

## Common Anti-Patterns (Do Not Do This)

- Repository per table
- IQueryable exposure from repositories
- Navigation properties across aggregates
- Business logic in handlers
- EF entities used directly as domain entities

These lead to:
- Tight coupling
- Hidden invariants
- Unmaintainable systems

---

## Why This Pattern Works in Real Enterprises

- Preserves business meaning
- Scales with complexity
- Enables performance tuning
- Survives team changes
- Aligns perfectly with CQRS + MediatR

---

## Trade-offs

**Pros**
- Clean domain model
- Predictable behavior
- Easier refactoring

**Cons**
- Higher upfront thinking
- Slightly more boilerplate
- Requires discipline

---

## Final Mental Model (Remember This)

- Aggregates protect business rules
- Repositories protect persistence boundaries
- Handlers orchestrate use cases
- Queries answer questions
- Events communicate change

If you internalize this, DDD will not confuse you again.

---

## Next Step

Proceed to **Domain Services & Cross-Aggregate Policies**  
File: `ea/domain-services.md`
