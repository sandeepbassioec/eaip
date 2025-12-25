# Architecture Constraints & Non-Negotiables
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document captures the **architectural constraints, guardrails, and
non-negotiable rules** that govern the design and evolution of EAVIP.

The intent of this document is to:
- Prevent architectural drift over time
- Ensure consistency across teams and implementations
- Make implicit assumptions explicit
- Serve as a long-term **reference contract** for architects and engineers

> Constraints are not limitations.  
> Constraints are **intentional boundaries that protect the architecture**.

---

## 1. Single Source of Truth Constraint

### Constraint
The **Enterprise Graph** is the single authoritative source of architectural truth.

### Why This Constraint Exists
Without a single source of truth:
- Diagrams drift
- Documents go stale
- Decisions become opinion-based

### Alternatives Considered
- Documents as truth
- Code as truth
- Diagrams as truth

### Why Rejected
Each alternative creates fragmentation and loss of trust over time.

### Enforced Rule
- All diagrams, reports, dashboards, and views are **derived**
- Manual editing of architecture views is prohibited

### Consequences
- Higher upfront modeling effort
- Long-term consistency and automation

---

## 2. Derived Views Only Constraint

### Constraint
All architectural views (logical, application, data, technology) must be
**projections of the Enterprise Graph**.

### Why This Constraint Exists
If views are editable independently:
- Conflicts arise
- Governance becomes impossible
- Drift cannot be detected

### Enforced Rule
- Views are read-only
- Changes occur only at the model level

### Consequences
- Tooling must support projection logic
- No diagram-driven architecture decisions

---

## 3. Core Domain Isolation Constraint

### Constraint
The **Enterprise Architecture Core** domain must not depend on:
- Platform concerns
- Infrastructure concerns
- UI or reporting concerns

### Why This Constraint Exists
Core architecture represents **business truth**, not implementation detail.

### Alternatives Considered
- Shared models across domains
- Platform-driven core logic

### Why Rejected
This leads to:
- Tight coupling
- Reduced longevity
- Vendor lock-in

### Enforced Rule
- Core domain emits events
- Other domains consume and adapt

---

## 4. Write Authority Constraint

### Constraint
Only the Core Domain is allowed to **mutate architectural facts**.

### Why This Constraint Exists
Multiple writers lead to:
- Conflicting ownership
- Inconsistent state
- Governance breakdown

### Enforced Rule
- Discovery, Reporting, Visualization are read-only
- All writes go through validated domain behavior

---

## 5. Read / Write Separation (CQRS) Constraint

### Constraint
Read and write responsibilities must be explicitly separated.

### Why This Constraint Exists
Architecture analytics is read-heavy and exploratory by nature.

### Alternatives Considered
- Unified CRUD model

### Why Rejected
- Poor performance at scale
- Complex models
- Hard to evolve

### Enforced Rule
- Commands mutate aggregates
- Queries use optimized read models

---

## 6. Aggregate Integrity Constraint

### Constraint
All state changes to domain data must occur through **Aggregate Roots**.

### Why This Constraint Exists
Direct entity manipulation:
- Breaks invariants
- Introduces hidden coupling
- Makes reasoning impossible

### Enforced Rule
- No public setters on entities
- Behavior-driven state changes only
- Repositories load/save aggregates only

---

## 7. Platform Configuration Immutability Constraint

### Constraint
Platform-level architectural decisions are immutable by default.

### Why This Constraint Exists
Platform assumptions affect:
- Reliability
- Security
- Cost
- Compliance

Frequent changes increase risk.

### Enforced Rule
- PlatformConfiguration is created during onboarding
- Mutations require explicit governance approval
- All changes are audited

---

## 8. Vendor Neutrality Constraint

### Constraint
No business or core architectural logic may depend on a specific cloud vendor
or proprietary service.

### Why This Constraint Exists
Vendor lock-in:
- Reduces adoption
- Increases long-term cost
- Limits customer trust

### Enforced Rule
- All external dependencies abstracted via adapters
- Cloud-specific services isolated in infrastructure layer

---

## 9. Security & Secret Handling Constraint

### Constraint
EAVIP must never store or manage customer secrets directly.

### Why This Constraint Exists
- Regulatory risk
- Liability exposure
- Trust erosion

### Enforced Rule
- Secrets referenced by identifiers only
- Integration with customer-managed secret systems
- No plaintext secrets in code or storage

---

## 10. Event Reliability Constraint

### Constraint
All domain events must be delivered reliably.

### Why This Constraint Exists
Architecture intelligence depends on complete and correct event streams.

### Enforced Rule
- Outbox Pattern is mandatory
- No direct event publishing after DB commit

---

## 11. Documentation & Reasoning Constraint

### Constraint
Every significant architectural decision must include explicit reasoning.

### Why This Constraint Exists
Future teams must understand:
- Why a decision was made
- What alternatives were rejected
- What trade-offs were accepted

### Enforced Rule
- Decisions recorded as ADRs
- No undocumented architectural changes

---

## 12. Human-in-the-Loop Constraint

### Constraint
Automation must never fully replace human architectural judgment.

### Why This Constraint Exists
Architecture is contextual and strategic, not purely mechanical.

### Enforced Rule
- Recommendations require approval
- Governance workflows are explicit
- Automation assists, not dictates

---

## Closing Notes

These constraints are **intentional design boundaries**.
Violating them may produce short-term convenience but will result in
long-term architectural decay.

This document must be reviewed before:
- Introducing new capabilities
- Refactoring core domains
- Changing deployment models
- Onboarding new enterprise customers
