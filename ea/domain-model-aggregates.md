# Domain Model, Aggregates & Repositories (DDD Execution Guide)
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document translates EAVIP’s architecture into a **Domain-Driven Design (DDD)
execution model**.

It answers the most practical questions developers struggle with:
- What is an entity vs aggregate vs aggregate root?
- How do we decide boundaries?
- Where does business logic live?
- How does this fit with CQRS, MediatR, and repositories?
- How do we avoid “logic scattered across handlers”?

This document is meant to be a **long-term reference** for real projects.

---

## Core DDD Principle (Locked)

> **Not everything that is a table is an aggregate.  
Not everything that is an entity deserves autonomy.**

DDD exists to:
- Protect business invariants
- Control change
- Reduce cognitive load

---

## Step 1 – Identify the True Domain

### In EAVIP, the Core Domain Is:
**Enterprise Architecture Knowledge & Decision Integrity**

Everything else (UI, reports, metrics, integrations) is **supporting or generic**.

---

## Step 2 – Bounded Contexts (Recap)

Each bounded context owns:
- Its language
- Its models
- Its rules
- Its data

Key bounded contexts for EAVIP:
- Architecture Core
- Governance
- Metrics & Intelligence
- Integration
- Platform Configuration

Aggregates **never cross bounded contexts**.

---

## Step 3 – Entity vs Aggregate vs Aggregate Root (Clear Rules)

### Entity
- Has identity
- Can change over time
- May or may not enforce invariants

**Example**
- ApplicationComponent
- DataFlow
- DeploymentNode

---

### Aggregate
A **consistency boundary**:
- A cluster of entities
- Must be consistent *together*
- Loaded and saved as a unit

---

### Aggregate Root
The **only entry point** to an aggregate.

Rules:
- External code talks ONLY to the root
- Root enforces invariants
- Child entities have no independent life

> Aggregate Root = Guardian of consistency

---

## Step 4 – How to Identify an Aggregate (Thumb Rules)

Ask these questions:

1. If I update this entity, must others update atomically?
2. Can this entity exist independently?
3. Who enforces business rules here?
4. What is the smallest unit of consistency?

If answers cluster → **one aggregate**.

---

## Step 5 – Concrete Aggregates in EAVIP

### 1. Application Aggregate (MOST IMPORTANT)

#### Aggregate Root
`Application`

#### Inside the Aggregate
- ApplicationComponent
- ApplicationSupportedEvent
- Internal Dependencies (within app)

#### Why This Is an Aggregate
- An application must always be internally consistent
- Components without an application make no sense
- Business rules live here (lifecycle, ownership, status)

---

### 2. ApplicationPortfolio Aggregate

#### Aggregate Root
`ApplicationPortfolio`

#### Inside
- Application references (by ID)
- Portfolio metrics
- Portfolio classification

#### Why Separate from Application
- Portfolio decisions are **strategic**
- Application is **operational**

Mixing both leads to bloated models.

---

### 3. DataFlow Aggregate

#### Aggregate Root
`DataFlow`

#### Inside
- Source
- Target
- Data classification
- Trust boundaries

#### Why Separate Aggregate
- Cross-application concern
- High governance impact
- Independent lifecycle

---

### 4. DeploymentModel Aggregate

#### Aggregate Root
`DeploymentModel`

#### Inside
- Nodes
- Environments
- Runtime topology

#### Why
Deployment changes frequently and independently from application logic.

---

### 5. PlatformConfiguration Aggregate

#### Aggregate Root
`PlatformConfiguration`

#### Inside
- Messaging mode
- Cache mode
- Secret references
- Deployment preferences

#### Why
This aggregate has **huge blast radius** → must be tightly controlled.

---

## Step 6 – What About Master Tables? (Very Important)

Examples:
- Country
- TechnologyCatalog
- ComplianceStandard

### Rule (Locked)
> Master data = **Reference Aggregates**

They:
- Have their own aggregate root
- Are referenced by ID only
- Are queried separately

Never embed them deeply into other aggregates.

---

## Step 7 – Handling UI Needs (Country Name Problem)

### Correct Pattern

- **Write Side**
  - Store `CountryId` only
  - Enforce invariants via ID

- **Read Side**
  - Join using read models
  - Or use denormalized projections

### Why
- Aggregates protect consistency
- Queries optimize usability
- Mixing both corrupts the model

---

## Step 8 – CQRS & Handlers (Your Confusion Answered)

### Command Handlers
- Orchestrate use cases
- Load aggregate
- Call aggregate methods
- Persist aggregate

> Command handlers are NOT aggregate roots.

---

### Aggregate Root
- Encapsulates business logic
- Exposes intention-revealing methods

Example:
```text
application.AddComponent(...)
application.Deprecate(...)
application.ChangeOwnership(...)
