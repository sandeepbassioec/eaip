# Service Decomposition & Domain-Aligned Architecture
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how EAVIP is decomposed into services and domains**
in a way that is:

- TOGAF-aligned (Phase D – Technology Architecture)
- DDD-aligned (Bounded Contexts & Aggregates)
- Enterprise-scalable
- Ready for gradual evolution (not premature microservices)

It answers:
> “What services exist, why they exist, and where the boundaries are?”

---

## Fundamental Decomposition Rule (Locked)

> **We decompose by BUSINESS CAPABILITY and DOMAIN OWNERSHIP,  
not by technology or CRUD operations.**

This is the most important rule in this document.

---

## Why Service Decomposition Matters

Without disciplined decomposition:
- Business logic spreads across handlers
- Ownership becomes unclear
- Changes ripple unpredictably
- Scaling becomes chaotic

Good decomposition enables:
- Independent evolution
- Clear responsibility
- Safer change
- Better reasoning

---

## Decomposition Strategy Chosen

### Strategy: Modular Monolith → Service-Ready Domains

We intentionally choose:

**NOT**
- Big ball of mud
- Premature microservices

**BUT**
- Strongly isolated domain modules
- Clear contracts
- Event-driven boundaries
- Infrastructure-ready separation

This allows:
- One deployment initially
- Many deployments later (if needed)

---

## Core Bounded Contexts (Services)

These are **logical services** (may run in same process initially).

---

## 1. Architecture Core Service (FOUNDATIONAL)

### Responsibility
- Own the **Enterprise Graph**
- Enforce architectural invariants
- Act as the single source of truth

### Owns Aggregates
- Enterprise
- Organization
- ApplicationPortfolio
- Application
- ApplicationComponent
- DataFlow
- Dependency
- DeploymentModel

### Why This Is a Separate Service
This domain:
- Must remain pure
- Must be stable
- Must not depend on platform or UI

> If this service is corrupted, the entire system loses trust.

---

## 2. Governance & Decision Service

### Responsibility
- Manage architecture decisions
- Enforce approval workflows
- Maintain ADRs
- Apply policies

### Owns Aggregates
- ArchitectureDecision (ADR)
- GovernancePolicy
- ApprovalWorkflow

### Why Separate from Core
- Governance rules change faster than architecture truth
- Enables governance maturity evolution
- Keeps core domain clean

---

## 3. Metrics & Intelligence Service

### Responsibility
- Calculate scores, indicators, and recommendations
- Generate “rework / rearchitect / sunset” signals
- Perform impact analysis

### Owns Aggregates
- ArchitectureMetric
- RiskIndicator
- CostValueIndicator

### Why Separate
- Computation-heavy
- Evolves frequently
- Must not mutate core architecture directly

---

## 4. Visualization & Modeling Service

### Responsibility
- Generate diagrams (C4, DFD, ER, Deployment)
- Support drill-down navigation
- Render views for stakeholders

### Owns Aggregates
- ArchitectureView
- DiagramDefinition
- LayoutMetadata

### Why Separate
- UI and visualization evolve rapidly
- Keeps rendering logic out of core domain

---

## 5. Integration & Event Exchange Service

### Responsibility
- Publish domain events
- Manage subscriptions
- Handle webhooks and queues
- Integrate with external systems

### Owns Aggregates
- IntegrationEndpoint
- Subscription
- EventContract

### Why Separate
- Integration is volatile
- Security-sensitive
- Infrastructure-dependent

---

## 6. Platform Configuration & Onboarding Service

### Responsibility
- Customer onboarding (SaaS / BYOC / On-Prem)
- Capture infra choices
- Manage secrets references
- Enforce platform constraints

### Owns Aggregates
- PlatformConfiguration
- EnvironmentProfile
- ConnectivityProfile

### Why Separate
- One-time + infrequent operations
- High blast radius if mixed with core logic

---

## 7. Reporting & Export Service

### Responsibility
- Generate reports
- Export data (PDF, Excel, JSON, XML)
- Provide executive views

### Owns Aggregates
- ReportDefinition
- ExportJob

### Why Separate
- Read-heavy
- Format-driven
- Must never affect core state

---

## Service Interaction Rules (Locked)

1. **No service directly updates another service’s aggregates**
2. Communication via:
   - Domain events
   - Explicit APIs
3. Core Architecture Service never depends on:
   - Reporting
   - Visualization
   - Integration

---

## Data Ownership Rules

| Service | Owns Data | Can Read Others |
|------|---------|----------------|
| Architecture Core | Yes | No |
| Governance | Yes | Core (read-only) |
| Metrics | Yes | Core (read-only) |
| Visualization | Yes | Core (read-only) |
| Integration | Yes | Core (read-only) |
| Reporting | Yes | Core (read-only) |

Ownership is **non-negotiable**.

---

## Why Not Microservices Yet?

### Rejected Option: Immediate Microservices

**Why Rejected**
- Operational overhead
- Premature scaling
- Increased failure modes

### Chosen Option: Service-Ready Modular Design

**Why Best**
- Clear boundaries
- Easier debugging
- Gradual evolution
- Enterprise-friendly

---

## Trade-offs

**Pros**
- Strong domain clarity
- Evolvable architecture
- Reduced coupling

**Cons**
- Requires discipline
- Boundary enforcement needed

---

## How This Helps You Practically

This decomposition:
- Maps cleanly to TOGAF Phase D
- Maps cleanly to DDD Bounded Contexts
- Prevents “logic scattered in handlers” problem
- Enables future microservices safely

---

## Closing Notes

Service decomposition is **not about deployment**.
It is about **ownership, responsibility, and reasoning**.

We now have:
- Clear services
- Clear boundaries
- Clear evolution path

---

## Next Logical Step

From here, the **only correct next step** is:

👉 **Deployment Architecture & Infrastructure Topology**  
(file: `ea/deployment-architecture.md`)

Say **`next`** and we go there.
