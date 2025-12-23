# Reference Implementation – Backend (Execution Guide)

## Purpose

This document provides a **practical, opinionated reference implementation**
for the **EAVIP backend**, aligned with all previously locked architecture decisions.

It answers:
- What services exist?
- How code is structured?
- How the Enterprise Graph is implemented?
- How APIs, events, and persistence fit together?

This is **not a framework mandate** — it is a **golden reference**.

---

## Technology Baseline (Reference)

> These are **recommended**, not hard dependencies.

- Language: Java / .NET (either is valid)
- API: REST (OpenAPI)
- Persistence: Graph abstraction + relational metadata
- Eventing: Adapter-based (Kafka/RabbitMQ/Cloud)
- Auth: OAuth2 / OIDC
- Build: Maven / Gradle / dotnet
- Containerization: Docker
- Orchestration: Kubernetes (optional for MVP)

---

## Service Decomposition (MVP)

### Services (Phase-1)

eavip-api-gateway
eavip-graph-service
eavip-governance-service
eavip-document-service
eavip-event-service


Each service:
- Owns its data
- Emits events
- Has strict boundaries

---

## API Gateway

### Responsibilities
- Authentication & authorization
- Tenant & time context injection
- Rate limiting
- Request validation
- Routing

### Non-Responsibilities
- Business logic
- Graph traversal
- Persistence

---

## Graph Service (Core)

### Responsibilities
- Enterprise Graph schema enforcement
- Node & relationship lifecycle
- Temporal validity
- Read-only traversal queries

### Package Structure (Example)
graph/
├── domain/
│ ├── nodes/
│ ├── relationships/
│ └── valueobjects/
├── application/
│ ├── commands/
│ ├── queries/
│ └── handlers/
├── infrastructure/
│ ├── persistence/
│ ├── events/
│ └── adapters/
└── api/


---

## Write Path (Strict)
API → Command → Validation → Governance Check
→ Event Emission → Persistence → Read Model Update

Rules:
- No direct writes from controllers
- No bypassing governance
- All writes are auditable

---

## Read Path (Optimized)
API → Query → Projection Store → Response

Characteristics:
- Read-only
- Cached where safe
- Time-context aware
- Tenant scoped

---

## Governance Service

### Responsibilities
- Policy evaluation
- Proposal workflows
- Approval tracking
- Violation detection

Governance is **called synchronously** on writes,
but **evaluated asynchronously** for insights.

---

## Document Service

### Responsibilities
- Markdown document storage
- ADR versioning
- Entity attachment
- Full-text indexing (optional later)

Documents are **data**, not comments.

---

## Event Service

### Responsibilities
- Event schema validation
- Adapter-based publishing
- Webhook delivery
- Retry & DLQ handling

### Event Rules
- Append-only
- Versioned
- Immutable
- Tenant scoped

---

## Persistence Strategy (Reference)

### Graph Data
- Abstract graph repository interface
- Backed by:
  - Native graph DB OR
  - Relational adjacency model

### Metadata & Governance
- Relational store

### Documents
- Object storage abstraction

---

## Security Model (Enforced Everywhere)

- OAuth2 / OIDC
- Scoped tokens
- Role-based access checks
- Service-to-service auth
- No shared secrets in code

---

## Configuration & Feature Flags

- Externalized configuration
- Feature flags for:
  - Governance enforcement
  - Advanced queries
  - Experimental features

---

## Observability (MVP-Level)

- Structured logging
- Correlation IDs
- Basic metrics
- Health endpoints

No heavy tracing in MVP.

---

## Testing Strategy

### Required
- Domain unit tests
- API contract tests
- Governance rule tests

### Optional (Later)
- Performance tests
- Chaos tests

---

## What This Reference Avoids

- Monolithic services
- Fat controllers
- Direct DB access from APIs
- Hidden coupling
- Framework lock-in

---

## Outcome

With this reference implementation:
- Teams can start coding immediately
- Architecture remains enforceable
- Governance cannot be bypassed
- Scale is achievable without rewrites

---

## Status

This document defines the **authoritative backend reference implementation guide**.

All backend development **should align** with this structure and flow.



