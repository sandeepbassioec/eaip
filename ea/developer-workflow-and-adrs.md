# Developer Workflow, ADRs & Daily Architecture Discipline
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how developers, architects, and teams work daily**
inside the EAVIP codebase **without breaking TOGAF intent or DDD boundaries**.

It answers:
- How work starts
- How decisions are made
- How changes are governed
- How architecture stays intact over years

This is **where theory becomes habit**.

---

## Core Principle (Locked)

**Architecture does not survive by documents.  
Architecture survives by workflow.**

If workflow is weak:
- ADRs rot
- Boundaries blur
- Discipline collapses

---

## Roles in Daily Execution

### 1. Enterprise Architect
- Owns architectural intent
- Reviews ADRs
- Validates TOGAF alignment
- Guards cross-context decisions

### 2. Solution / Domain Architect
- Designs bounded contexts
- Owns aggregates and invariants
- Authors ADRs for domain changes

### 3. Developer
- Implements within boundaries
- Proposes changes via ADR
- Never bypasses architecture tests

### 4. Tech Lead
- Enforces workflow discipline
- Reviews PRs for architectural impact
- Ensures learning is retained

---

## Daily Developer Workflow (Authoritative)

### Step 1 – Understand Context Before Coding

Before writing **any code**, the developer must know:
- Which bounded context
- Which aggregate
- Which capability
- Which TOGAF phase it impacts

If unclear → stop.

---

### Step 2 – Identify Change Type

Every task falls into **one** category:

1. Pure implementation (no decision)
2. Local design decision
3. Cross-aggregate decision
4. Cross-bounded-context decision
5. Platform-level architectural decision

Only #1 requires **no ADR**.

---

## Architecture Decision Records (ADR)

### What Is an ADR

An ADR is a **permanent architectural memory**.

It captures:
- Decision
- Reason
- Alternatives
- Trade-offs
- Consequences

No ADR → no merge.

---

### ADR Location

/ea/docs/adr/
ADR-0001-platform-bootstrap.md
ADR-0002-graph-as-source-of-truth.md


---

### ADR Lifecycle

1. Proposed
2. Reviewed
3. Accepted
4. Implemented
5. Superseded (never deleted)

History is immutable.

---

## When ADR Is Mandatory (Non-Negotiable)

ADR is required when:
- Creating a new bounded context
- Changing aggregate boundaries
- Introducing a new integration
- Changing consistency model
- Introducing new infrastructure dependency
- Violating an existing rule (with justification)

---

## ADR Template (Standardized)

```md
# ADR-XXXX: <Title>

## Status
Proposed | Accepted | Superseded

## Context
What problem exists?

## Decision
What was decided?

## Alternatives Considered
Option A  
Option B  

## Rationale
Why this option?

## Trade-offs
What is gained and lost?

## Consequences
Short-term and long-term impact
```
