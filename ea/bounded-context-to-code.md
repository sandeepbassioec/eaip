# Bounded Context → Code & Service Boundary Mapping
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document translates **Domain-Driven Design (DDD) bounded contexts**
into **concrete code, module, and service boundaries**.

It is the **most critical execution document** because it answers:

- How abstract architecture becomes real code
- Where boundaries are enforced technically
- How to prevent accidental coupling
- How today’s monolith becomes tomorrow’s services
- Why this structure maximizes long-term learning and scalability

This document exists to ensure **architecture survives implementation**.

---

## Core Principle (Locked)

**Bounded Context boundaries must be enforced in code, not in documentation.**

If boundaries are not enforced technically:
- They will be violated
- Architecture will decay
- Learning will collapse

---

## Chosen Execution Model (Locked)

### Modular Monolith — Architecture-Enforced

This means:
- Single deployable (initially)
- Multiple **strictly isolated modules**
- Explicit dependency rules
- Clear evolution path to services

---

## Why Modular Monolith Is the Right Choice (WHY)

### Alternatives Considered

#### Microservices from Day-1 ❌
Rejected because:
- Introduces operational complexity too early
- Obscures domain learning
- Makes DDD harder to understand
- Shifts focus to DevOps instead of architecture

#### Pure Monolith ❌
Rejected because:
- Encourages shared models
- Hides bounded context violations
- Makes future extraction painful

---

### Why Modular Monolith Wins ✅

- Enforces boundaries **without operational noise**
- Keeps learning focused on **DDD concepts**
- Makes dependencies explicit
- Allows gradual, safe evolution
- Matches how mature enterprises actually start

This is the **ideal learning + production balance**.

---

## Bounded Contexts (Recap)

The following bounded contexts are **locked**:

1. Architecture Core
2. Architecture Decisions & Governance
3. Metrics & Intelligence
4. Visualization & Diagrams
5. Platform Configuration

Each bounded context maps to **exactly one code module**.

---

## Code-Level Mapping Rules (Locked)

### Rule 1: One Bounded Context = One Code Module

Each module:
- Has its own domain model
- Has its own aggregates
- Has its own repositories
- Owns its persistence
- Emits its own domain events

No shared domain models across modules.

---

### Rule 2: No Cross-Context Direct Calls

Forbidden:
- Direct method calls
- Shared entities
- Shared repositories
- Shared database tables

Allowed:
- Domain events
- Explicit APIs
- Anti-Corruption Layers (ACL)

---

## Proposed Solution Structure (.NET)

/src
/Architecture.Core
/Domain
/Application
/Infrastructure
/API

/Architecture.Governance
/Domain
/Application
/Infrastructure
/API

/Architecture.Metrics
/Domain
/Application
/Infrastructure
/API

/Architecture.Visualization
/Domain
/Application
/Infrastructure
/API

/Platform.Configuration
/Domain
/Application
/Infrastructure
/API

/Shared.Kernel


---

## Layer Responsibilities (Critical for DDD Learning)

### Domain Layer
- Aggregates
- Value Objects
- Domain Events
- Domain Services
- Business invariants

No infrastructure references allowed.

---

### Application Layer
- Command handlers
- Query handlers
- Process Managers (Sagas)
- Orchestration logic

No business rules here.

---

### Infrastructure Layer
- EF Core / Dapper
- Messaging adapters
- External integrations
- Persistence implementations

Replaceable, testable, isolated.

---

### API Layer
- Controllers
- Request/Response DTOs
- Authentication & authorization
- OpenAPI contracts

No domain logic.

---

## Shared Kernel (Very Small by Design)

Allowed:
- Strongly-typed IDs
- Time abstractions
- Base domain interfaces

Forbidden:
- Aggregates
- Entities
- Business rules
- Repositories

The smaller the Shared Kernel, the healthier the system.

---

## Dependency Rules (Compile-Time)

Allowed dependencies:

- API → Application
- Application → Domain
- Infrastructure → Application + Domain

Forbidden dependencies:
- Domain → Application
- Domain → Infrastructure
- Cross-context Domain references

These rules must be enforced via tooling.

---

## Runtime Communication Model

### Intra-Monolith
- Domain Events
- In-memory dispatch (initially)

### Inter-Context
- Explicit event contracts
- Async by default
- Eventually consistent

This mirrors future microservice communication.

---

## Database Strategy (Phase-1)

- One database per bounded context (logical)
- No cross-context joins
- No shared tables
- Context-owned schemas

This makes future extraction straightforward.

---

## Evolution to Microservices (Planned)

### When to Extract a Context

- Independent scaling needed
- Separate ownership required
- Regulatory isolation needed
- Operational boundaries justified

### How Extraction Happens

- Event contracts already exist
- APIs already explicit
- Persistence already isolated

Extraction becomes a **deployment change**, not a redesign.

---

## Guardrails to Prevent Boundary Violations

- Architecture tests
- Dependency rule enforcement
- Code reviews tied to contexts
- CI checks for forbidden references

Architecture must fail fast if violated.

---

## Trade-offs (Explicit)

### Pros
- Maximum learning clarity
- Strong architectural discipline
- Safe evolution
- Low operational risk

### Cons
- Requires discipline
- Slight upfront planning
- Engineers must respect rules

These trade-offs are **deliberately accepted**.

---

## Why This Is Ideal for You

- You learn DDD **correctly**
- You see TOGAF **executed in code**
- You avoid premature complexity
- You gain skills transferable to any enterprise

This structure can scale to **100,000+ classes** safely.

---

## Final Mental Model

- Bounded Context = Module
- Module = Ownership
- Ownership = Safety
- Safety = Evolution

---

## Next Step

Proceed to **Walking Skeleton Definition**
— the first real, end-to-end executable slice.

File: `ea/walking-skeleton.md`
