# Repository Structure, Coding Standards & Module Boundaries

## Purpose

This document defines:
- The **repository structure**
- **Module and ownership boundaries**
- **Coding and contribution standards**

Its goal is to ensure:
- Long-term maintainability
- Parallel team development
- Architectural integrity at scale

This document is authoritative for all contributors.

---

## Guiding Principles

1. Structure follows **bounded contexts**
2. Modules are **independently evolvable**
3. Dependencies point **inward**
4. No cross-context code sharing
5. Standards are enforced automatically

---

## 1. Repository Structure

The repository is organized by **bounded context**, not by technical layers.

/docs
requirements.md
system-decomposition.md
context-apis-and-events.md
internal-domain-models.md
domain-policies-and-workflows.md
high-level-architecture.md
api-gateway-and-interaction-flows.md
deployment-and-release-strategy.md
repository-structure-and-standards.md

/src
/identity-access
/workspace
/application-portfolio
/semantic-tagging
/adr
/architecture-modeling
/cloud-capability
/roadmap-transformation
/event-exchange
/activity-audit

/shared
/kernel
/contracts

/tests
/unit
/integration
/contract


---

## 2. Bounded Context Module Structure

Each bounded context follows the same internal layout:

/<bounded-context>
/domain
/aggregates
/entities
/value-objects
/events
/policies
/application
/commands
/queries
/handlers
/interfaces
/api
/events
/infrastructure

### Rules
- `domain` has **no dependencies**
- `application` depends on `domain`
- `interfaces` depends on `application`
- `infrastructure` depends on abstractions only

---

## 3. Shared Modules

### 3.1 Shared Kernel

/shared/kernel

Contains:
- Primitive value types (IDs, timestamps)
- Error types
- Base abstractions

**Rules**
- Extremely small
- No business logic
- Changes require architecture review

---

### 3.2 Contracts

/shared/contracts

Contains:
- Event schemas
- API DTOs
- Integration payload definitions

**Rules**
- Immutable once published
- Versioned explicitly
- Backward compatibility enforced

---

## 4. Dependency Rules (STRICT)

### Allowed
- Intra-context dependencies
- Shared kernel usage
- Contract consumption

### Forbidden
- Cross-context domain references
- Shared databases
- Utility dumping grounds

Violation = **build failure**

---

## 5. Coding Standards

### General
- Clear naming using ubiquitous language
- No abbreviations unless universally accepted
- Explicit intent over cleverness

### Domain Layer
- No framework annotations
- No infrastructure concerns
- Invariants enforced inside aggregates

### Application Layer
- One command/query per handler
- No business logic duplication
- Policies invoked explicitly

---

## 6. Event Standards

- Events are immutable
- Events use past tense naming
- Payloads are explicit and minimal
- Version changes are additive only

---

## 7. API Standards

- APIs are versioned
- Backward compatibility is mandatory
- Validation happens at boundaries
- No leaking internal models

---

## 8. Testing Strategy

### Test Types
- Unit tests (domain logic)
- Integration tests (context boundaries)
- Contract tests (events and APIs)

### Rules
- Domain invariants must be tested
- Breaking a contract test blocks release
- No shared test utilities across contexts

---

## 9. Code Ownership & Reviews

Each bounded context has:
- Clear owning team
- Mandatory reviewers
- Independent release authority

Cross-context changes require:
- Explicit architecture approval
- Documentation update

---

## 10. Documentation Rules

- All architectural changes update `/docs`
- Code without documentation is incomplete
- Diagrams and ADRs must be referenced

---

## 11. Forbidden Practices

- God modules
- Utility dumping
- Cross-context shortcuts
- Implicit behavior
- Silent breaking changes

---

## Status

This document defines the **official repository structure and development standards**.

All contributions must comply to ensure system integrity and long-term success.

