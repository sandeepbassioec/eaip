# Walking Skeleton – First Executable Slice
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines the **Walking Skeleton** for EAVIP.

A Walking Skeleton is the **smallest possible, end-to-end, production-quality slice**
of the system that proves:

- Architecture is executable
- Boundaries are correct
- Technology choices work together
- The platform can evolve safely

This is **not a prototype** and **not a spike**.
It is the foundation on which everything else will grow.

---

## Core Principle (Locked)

**If architecture cannot run, it does not exist.**

The Walking Skeleton must:
- Touch every major architectural layer
- Respect all bounded context boundaries
- Be deployable
- Be testable
- Be evolvable

---

## Why Walking Skeleton Comes Now (WHY)

At this point we have:
- TOGAF architecture completed
- DDD boundaries locked
- Execution model finalized

What we do **not yet have** is proof that:
- These decisions work together in real code
- Teams can follow them without confusion
- The architecture is not fragile

The Walking Skeleton answers all of that **early**.

---

## What the Walking Skeleton Is (and Is Not)

### It IS:
- One real business flow
- One real API
- One real aggregate
- One real database schema
- One real UI interaction

### It IS NOT:
- Feature-complete
- Optimized
- Fully styled
- Comprehensive

Its purpose is **structural validation**, not functionality.

---

## Selected Bounded Context for the Skeleton

### Chosen Context: **Architecture Core**

### Why This Context

- It is foundational
- All other contexts depend on it
- It contains the primary domain language
- It validates most architectural assumptions early

If this context works, others will follow cleanly.

---

## Selected Business Flow (Minimal but Real)

### Flow: **Create Application in an Organization**

End-to-end steps:

1. User creates an Organization
2. User creates an Application under that Organization
3. Application is persisted
4. Domain events are emitted
5. Read model reflects the change
6. UI displays the result

This flow exercises:
- Domain modeling
- Aggregate rules
- Persistence
- Events
- API contracts
- UI wiring

---

## Domain Model (Skeleton Scope)

### Aggregate Root: `Application`

Responsibilities:
- Ensure application identity
- Enforce invariants
- Control lifecycle
- Emit domain events

### Supporting Entities / Value Objects
- `ApplicationId`
- `OrganizationId`
- `ApplicationName`
- `LifecycleState`

No extra concepts are allowed in the skeleton.

---

## Application Layer Responsibilities

- Command: `CreateApplication`
- Handler:
  - Loads Organization (by ID only)
  - Creates Application aggregate
  - Persists via repository
  - Publishes domain events

No business logic outside the aggregate.

---

## Persistence Strategy (Skeleton)

- EF Core (initially)
- One schema owned by Architecture Core
- No cross-context joins
- Schema reflects aggregate boundaries

Persistence is **replaceable**, not embedded.

---

## API Layer (Skeleton)

### Endpoint
POST /organizations/{organizationId}/applications

Responsibilities:
- Input validation
- Authentication / authorization
- Mapping DTO → Command
- Returning response DTO

No domain logic here.

---

## Event Flow (Skeleton)

On successful creation:
- `ApplicationCreated` domain event is raised
- Event is handled internally
- Future external publishing is simulated

This validates event-driven design early.

---

## Read Model (Skeleton)

- Simple query returning:
  - Application ID
  - Application Name
  - Organization ID
  - Lifecycle State

Read model is **separate** from write model.

---

## UI Slice (Skeleton)

- Simple form:
  - Application Name
- Submit action
- Success view:
  - Shows created application

No complex UX.
No diagrams yet.
Just proof of flow.

---

## What Is Explicitly Excluded (On Purpose)

- Metrics & scoring
- Governance workflows
- Advanced security
- Import/export
- Diagrams
- Observability dashboards

Adding these now would dilute learning.

---

## Validation Criteria (Definition of Done)

The Walking Skeleton is complete when:

- Code compiles with enforced boundaries
- One application can be created end-to-end
- Domain invariants are enforced
- Events are emitted
- UI reflects real backend state
- Architecture rules are not violated

If any rule is broken, the skeleton fails.

---

## Trade-offs (Explicit)

### Pros
- Fast feedback
- Early risk detection
- Architecture validation
- Learning acceleration

### Cons
- Limited functionality
- No immediate business value
- Requires discipline

These trade-offs are intentional and accepted.

---

## Why This Works for Learning DDD & TOGAF

- You see abstract ideas become concrete
- You learn where mistakes actually happen
- You understand the cost of violations
- You gain confidence before scaling

This is **how real enterprise systems should start**.

---

## Final Mental Model

- Small but real
- Correct before complete
- Structure before scale
- Learning before optimization

---

## Next Step

Proceed to **Backend Reference Architecture (Skeleton Implementation)**

File: `ea/backend-reference-architecture.md`


