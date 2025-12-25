# Data Storage Strategy & Persistence Patterns
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how data is stored, owned, accessed, and evolved**
within EAVIP.

It answers:
- What data stores exist and why
- Which service owns which data
- How consistency is maintained
- How historical truth is preserved
- How reads scale without corrupting writes

This aligns with:
- TOGAF Phase D (Technology Architecture)
- DDD Aggregates & Repositories
- CQRS principles

> Bad persistence decisions silently destroy good architectures.

---

## Core Persistence Principles (Locked)

1. **Data ownership is explicit**
2. **No shared databases across services**
3. **Write models prioritize integrity**
4. **Read models prioritize usability**
5. **History is immutable**
6. **Queries must never corrupt domain intent**

These principles override convenience.

---

## Storage Types Overview

EAVIP intentionally uses **multiple data models**:

| Purpose | Storage Type |
|------|--------------|
| Transactional writes | Relational DB |
| Dependency traversal | Graph DB |
| Search & analytics | Search engine |
| Performance acceleration | Cache |
| Event durability | Outbox tables |

Each exists for a reason.

---

## 1. Relational Database (System of Record)

### Role
Primary system of record for **domain state**.

### Stores
- Aggregates
- Entity state
- Decisions
- Governance workflows
- Platform configuration

### Why Relational
- Strong consistency
- Transactional guarantees
- Clear constraints
- Mature tooling

### Alternatives Considered
- NoSQL only
- Event store only

**Rejected because**
- Harder invariants
- Operational complexity
- Poor reporting ergonomics

---

## 2. Graph Database (Architecture Relationships)

### Role
Store and query **architecture relationships** efficiently.

### Stores
- Dependencies
- Data flows
- Component relationships
- Impact paths

### Why Graph
Architecture questions are graph problems:
- “What breaks if this changes?”
- “What depends on X?”
- “Where does data flow?”

Relational joins do not scale for this.

---

## 3. Search & Analytics Store

### Role
Support:
- Full-text search
- Time-based analysis
- Executive dashboards
- Reporting

### Why Separate
- Optimized for reads
- Does not affect transactional workloads
- Enables denormalized views

---

## 4. Read Models (CQRS)

### Core Rule
> **Read models are projections, not truth.**

### Characteristics
- Denormalized
- Optimized for UI
- Disposable and rebuildable
- Eventually consistent

### Why CQRS Is Mandatory Here
Architecture platforms are:
- Read-heavy
- Exploratory
- Multi-stakeholder

Mixing read/write models leads to:
- Bloated entities
- Complex logic
- Fragile systems

---

## 5. Outbox Pattern (Event Reliability)

### Why Outbox Exists
To guarantee:
- No lost events
- No partial commits
- No race conditions

### How It Works
1. Domain change commits
2. Event written to outbox table
3. Separate dispatcher publishes event
4. Event marked as delivered

This is **non-negotiable**.

---

## 6. Temporal & Historical Data

### Rule (Locked)
> EAVIP never overwrites history.

### Why
Auditors and architects care about:
- What was true at time T
- What was known when a decision was made

### Implementation
- Valid-from / valid-to timestamps
- Versioned records
- Append-only logs

---

## 7. Caching Strategy

### Purpose
- Performance optimization
- Never correctness

### Rules
- Cache invalidation via events
- No writes through cache
- Cache failures must not break correctness

---

## 8. Data Access Rules (Strict)

| Rule | Reason |
|----|------|
| No cross-service DB access | Prevent coupling |
| Repositories return aggregates | Preserve invariants |
| Queries bypass aggregates | Performance & simplicity |
| IDs, not objects across boundaries | Avoid entanglement |

---

## 9. Handling Reference / Master Data

### Examples
- Country
- Currency
- Technology catalogs
- Standards

### Strategy
- Treated as **separate aggregates**
- Referenced by ID only
- Queried separately when needed

### Why
Prevents aggregate explosion and hidden coupling.

---

## 10. Consistency Model

### Write Side
- Strong consistency
- Transactions enforced

### Read Side
- Eventual consistency
- Tolerates short delays

This balance is intentional.

---

## Trade-offs

**Pros**
- High data integrity
- Scalable reads
- Clear ownership
- Audit-ready

**Cons**
- More storage systems
- Requires discipline
- Slightly higher complexity

---

## Why This Strategy Is Best

- Matches real enterprise architecture needs
- Aligns with DDD & CQRS
- Enables long-term evolution
- Avoids “one DB to rule them all” trap

---

## Closing Notes

Persistence is not an implementation detail.
It is **architecture**.

These rules ensure:
- Trustworthy architecture intelligence
- Safe evolution
- Long-term maintainability

---

## Next Logical Step

👉 **Security Architecture & Zero Trust Model**  
(file: `ea/security-architecture.md`)

Say **`next`** and we continue.
