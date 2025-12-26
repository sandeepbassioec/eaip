# Bounded Context → Code Mapping Strategy
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document explains **how Domain-Driven Design (DDD) bounded contexts
are translated into real, enforceable code structure** for EAVIP.

It answers:
- How we convert architecture into folders, assemblies, and services
- How boundaries are enforced technically (not by convention)
- Why this structure survives scale, teams, and time

This is the **bridge between TOGAF Phase C and real software construction**.

---

## Core Principle (Locked)

**Bounded Contexts are architectural firewalls.  
Code structure must make violations difficult, not easy.**

If boundaries rely on discipline alone, they will fail.

---

## What Is a Bounded Context (Practical View)

A bounded context is:
- A **semantic boundary**
- A **decision boundary**
- A **consistency boundary**
- A **deployment and ownership boundary**

Inside a bounded context:
- Language is consistent
- Invariants are enforced
- Models are valid

Across bounded contexts:
- Integration is explicit
- Consistency is eventual
- Translation is required

---

## Identified Core Bounded Contexts in EAVIP

The following bounded contexts are **explicitly locked**:

1. Core Architecture Context
2. Discovery & Ingestion Context
3. Metrics & Decision Intelligence Context
4. Visualization & Modeling Context
5. Architecture Decision & Governance Context
6. Reporting & Export Context
7. Integration & Event Exchange Context
8. Platform Configuration Context

Each context has **clear ownership and authority**.

---

## Mapping Rule: One Context → One Code Boundary

### Mandatory Mapping

Each bounded context maps to:
- One solution folder
- One primary assembly
- One persistence model
- One API surface (or none if internal)

Example:
/src
/CoreArchitecture
/DiscoveryIngestion
/MetricsIntelligence
/VisualizationModeling
/ArchitectureGovernance
/ReportingExport
/IntegrationExchange
/PlatformConfiguration


No shared domain models.

---

## Internal Structure of a Bounded Context

Every bounded context follows the same internal structure.
/CoreArchitecture
/Domain
/Aggregates
/Entities
/ValueObjects
/Events
/Services
/Application
/Commands
/Queries
/Handlers
/DTOs
/Infrastructure
/Persistence
/Repositories
/Adapters
/API


---

## Why This Structure Exists (Reasoning)

### Why Separate Domain from Application?
- Domain = business truth
- Application = orchestration
- Keeps business rules stable

### Why Infrastructure Is Isolated?
- Enables vendor neutrality
- Supports SaaS / BYOC / On-Prem
- Prevents infra leakage into domain

### Why API Is Thin?
- APIs are delivery mechanisms
- Not owners of logic

---

## Aggregate Enforcement Rules

Inside each bounded context:

- Aggregates enforce invariants
- Aggregate Roots are the only mutation entry points
- No aggregate references another aggregate by object
- Only ID-based references allowed

This prevents **implicit coupling**.

---

## Cross-Bounded Context Communication

### Allowed Methods

- Domain Events
- Integration Events
- Read Models (Query side only)
- Explicit Anti-Corruption Layers (ACL)

### Forbidden Methods

- Direct repository access
- Shared database tables
- Shared ORM entities
- Cross-context transactions

---

## Consistency Model (Explicit)

| Scope | Consistency |
|-----|-------------|
| Inside Aggregate | Strong |
| Inside Context | Transactional |
| Across Contexts | Eventual |

This is intentional and non-negotiable.

---

## Anti-Corruption Layer (ACL)

Whenever one bounded context consumes another:

- Translation layer is mandatory
- No leaking foreign models
- Semantic mismatches handled explicitly

Why:
- Protects core domain purity
- Allows independent evolution

---

## Example: Dependency Flow
Discovery Context
emits
ArchitectureDiscoveredEvent
↓
Core Architecture Context
validates
persists
emits
ArchitectureChangedEvent


No direct calls.
No shared models.

---

## Why Not a Shared Kernel?

Rejected because:
- EAVIP is multi-domain
- Evolution speed differs per context
- Shared kernels rot over time

Trade-off accepted:
- Slight duplication
- Massive long-term clarity

---

## Architectural Guardrails (Enforcement)

- Assembly reference rules
- Architecture tests
- CI gate checks
- ADR enforcement

Violations fail builds.

---

## Common Mistakes (Avoid)

- “Just reuse this entity”
- “It’s faster to call directly”
- “We’ll refactor later”
- “This is only reporting”

These destroy architecture silently.

---

## How This Supports TOGAF

- Phase C artifacts become executable
- Architecture becomes enforceable
- Change impact is predictable
- Governance becomes real

---

## Learning Outcome (For You)

By following this:
- You internalize DDD naturally
- You stop designing accidental monoliths
- You understand architecture as constraint, not ceremony

---

## Trade-offs (Explicit)

### Benefits
- Extreme clarity
- Parallel team execution
- Long-term resilience

### Costs
- More code
- Slower early velocity
- Higher upfront thinking

These are **strategic investments**.

---

## Next Step

Proceed to **Architecture Execution Readiness & Software Construction Strategy**

File: `ea/architecture-execution-readiness.md`
