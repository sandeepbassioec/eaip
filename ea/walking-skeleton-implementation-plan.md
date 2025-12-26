# Walking Skeleton – Implementation Plan (EAVIP)

## Purpose

This document defines the **concrete, step-by-step execution plan** for building
the first working slice of the **Enterprise Architecture Visibility & Intelligence Platform (EAVIP)**.

This is **not** a conceptual document.

This is the point where:
- TOGAF moves from **architecture definition → execution**
- DDD moves from **models → running code**
- Learning moves from **theory → muscle memory**

The Walking Skeleton is intentionally minimal but end-to-end.

---

## What a “Walking Skeleton” Means (WHY)

A Walking Skeleton is:

- A **thin, vertical slice** across all layers
- From UI → API → Domain → Persistence → Diagram → Query
- With **real architecture rules enforced**
- Even if functionality is extremely small

We do this because:
- Architecture correctness matters more than feature completeness
- Early feedback prevents large-scale rework
- DDD concepts only make sense when executed, not discussed

---

## What This Walking Skeleton Will Prove

At the end of this plan, EAVIP will be able to:

1. Create a minimal **Enterprise**
2. Persist it via a **DDD Aggregate + Repository**
3. Emit a **Domain Event**
4. Store it in the **Enterprise Graph**
5. Render a **basic diagram**
6. Query it back via a **read-only API**
7. Display it in a **minimal UI**

Nothing more. Nothing less.

---

## Explicit Non-Goals (IMPORTANT)

The following are **intentionally excluded**:

- Metrics
- Decision indicators
- Governance workflows
- Security policies
- Multi-org hierarchy
- Import/export
- Advanced diagrams
- AI / intelligence features

If something is not needed to validate architecture flow, it is excluded.

---

## Execution Order (Non-Negotiable)

Implementation must follow **this exact order**:

1. Domain
2. Persistence
3. Application Layer
4. API
5. Query Model
6. Visualization
7. UI

Skipping layers or reordering breaks architectural learning.

---

## Step 1: Define the First Bounded Context

### Context Name
**Core Architecture Context**

### Responsibility
Owns canonical enterprise structure.

### First Aggregate
**Enterprise**

---

## Step 2: Define the Aggregate (DDD)

### Aggregate Root
`Enterprise`

### Why Enterprise First?
- Top of the drill-down hierarchy
- Minimal dependencies
- Ideal for learning aggregate rules

### Enterprise Aggregate Rules
- Has a stable identity
- Owns its own invariants
- No external entity references
- Emits domain events

### Fields (Minimal)
- EnterpriseId
- Name
- Description
- CreatedAt

---

## Step 3: Define the Domain Event

### Event
`EnterpriseCreated`

### Why Events Now?
Because:
- EAVIP is event-driven by design
- We must learn eventual consistency early
- Downstream systems depend on events

### Event Payload (Minimal)
- EnterpriseId
- Name
- OccurredAt

---

## Step 4: Repository Design

### Repository Interface
`IEnterpriseRepository`

### Rules
- Repository returns only Aggregates
- No ORM leakage into domain
- No query logic here

### Methods
- Add(Enterprise)
- GetById(EnterpriseId)

---

## Step 5: Persistence (Infrastructure)

### Technology Choice
- PostgreSQL (reference)
- OR Neo4j later (not now)

### Why Relational First?
- Simpler debugging
- Clear transaction boundaries
- Graph comes later

### Tables
- enterprises
- domain_events (outbox-style)

---

## Step 6: Application Layer (CQRS)

### Command
`CreateEnterpriseCommand`

### Command Handler
`CreateEnterpriseCommandHandler`

### Responsibilities
- Validate input
- Call Aggregate constructor
- Persist via repository
- Commit transaction
- Publish Domain Event

No business logic leaks outside the aggregate.

---

## Step 7: API Layer

### Endpoint
POST /api/enterprises


### API Responsibility
- Translate HTTP → Command
- No business logic
- No persistence logic

---

## Step 8: Query Model (READ SIDE)

### Why Separate Query Model?
Because:
- Reads ≠ Writes
- UI needs denormalized data
- Domain purity must be preserved

### Query
GET /api/enterprises/{id}


### Implementation Options
- SQL View
- Dapper
- Read-only EF model

Navigation properties are allowed **only here**.

---

## Step 9: Minimal Visualization

### Diagram Type
- C4 Context (Enterprise only)

### Source of Truth
- Enterprise Graph
- Derived from canonical data

No manual diagram drawing.

---

## Step 10: Minimal UI

### Screen
- Create Enterprise
- View Enterprise box

### Purpose
- Prove full vertical flow
- Not aesthetics

---

## Validation Checklist (MANDATORY)

You may proceed to next capability only if:

- [ ] Aggregate enforces invariants
- [ ] Domain Event is emitted
- [ ] Repository hides persistence
- [ ] Command has no business logic
- [ ] Query does not touch domain
- [ ] Diagram is auto-derived
- [ ] UI uses query API only

If any checkbox fails → stop.

---

## Learning Outcomes (WHY This Matters)

After this skeleton, you will **fully understand**:

- Aggregate vs Entity
- Command vs Domain Logic
- Why repositories exist
- Why queries bypass domain
- Event-driven thinking
- TOGAF → DDD → Code traceability

This is the **foundation** for everything else.

---

## What Comes After This (Preview)

Once the skeleton is stable, we will:

1. Add **Organization** aggregate
2. Introduce **Dependencies**
3. Add **Data Flows**
4. Introduce **Decision Indicators**
5. Add **Governance workflows**
6. Scale to full enterprise modeling

But only **after** this works flawlessly.

---

## Architectural Principle Reinforced

> “If you cannot build it simply,
> you do not understand it deeply enough.”

This Walking Skeleton is your **proof of understanding**.
