# Technology Stack & Architecture Choices (.NET / C# First)

## Purpose

This document defines the **authoritative technology stack and concrete architecture choices**
for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP),
with **.NET Core and C# as the primary backend technology**.

It ensures:
- Strong on-prem compatibility
- Enterprise-grade stability
- Cloud-neutral deployment
- Long-term maintainability without niche skills

This is the **technical execution contract** for engineering.

---

## Technology Selection Principles (Locked)

1. Enterprise-proven over fashionable
2. On-Prem compatibility is mandatory
3. Cloud-neutral by architecture
4. Replaceable infrastructure via adapters
5. Predictable performance over magic
6. Strong typing and tooling preferred

---

## High-Level Architecture Pattern

- Modular Monolith (Phase-1)
- Clear bounded contexts
- API-first
- Event-driven where required
- Stateless services
- Strong persistence boundaries

Microservices are a **future option**, not a Phase-1 requirement.

---

## Backend Stack (Authoritative)

### Language & Runtime

- **Primary:** .NET 8 (LTS) / .NET Core
- **Language:** C#
- **Rationale:**
  - Excellent on-prem support
  - Mature enterprise ecosystem
  - Strong async & performance model
  - Rich tooling (Visual Studio, Rider)
  - Long-term Microsoft support

This is **non-negotiable** for Phase-1.

---

### Web Framework

- **ASP.NET Core**
- REST APIs
- Middleware-based pipeline
- Validation via filters
- Policy-based authorization

---

### Graph Persistence

- **Primary:** Neo4j (Self-managed)
- **Access via:** Neo4j .NET Driver
- **Usage:**
  - Enterprise Graph
  - Dependencies
  - Temporal relationships
  - Impact analysis

### Abstraction Rule
- Domain code depends on **IGraphRepository**
- No Cypher leaks outside infrastructure layer
- Neo4j is replaceable in future

---

### Relational Storage

- **PostgreSQL**
- Access via **Entity Framework Core**

Used for:
- Governance workflows
- Proposals & approvals
- Users & roles
- Audit metadata
- Document metadata

---

### Search & Indexing

- **OpenSearch**
- Access via REST client

Used for:
- Full-text document search
- Metadata indexing
- Audit and activity queries

---

### Messaging / Eventing

**Adapter-based abstraction (MANDATORY)**

Supported implementations:
- Kafka
- RabbitMQ
- ActiveMQ
- IBM MQ

Rules:
- Core domain never depends on vendor SDKs
- Message contracts are versioned
- Event delivery is async-only

---

## Frontend Stack (Authoritative)

### Framework

- **React**
- **TypeScript**
- Strict typing enforced

---

### State Management

- URL-driven state
- Explicit view context
- Minimal global state
- Server is always the source of truth

---

### Diagram Rendering

- Custom SVG / Canvas-based renderer
- Deterministic layout algorithms
- No embedded third-party diagram editors
- Diagrams are always derived, never edited

---

## API Design

- REST (JSON)
- Command / Query separation
- Versioned endpoints
- OpenAPI (Swagger) mandatory
- No graph query language exposed externally

---

## Authentication & Authorization

- OAuth2 / OpenID Connect
- JWT access tokens
- RBAC + policy-based authorization
- Tenant isolation enforced at middleware + domain level

---

## Deployment & Platform

### Containerization
- Docker

### Orchestration
- Kubernetes (preferred)
- Docker Compose (local / demo)

---

### Infrastructure-as-Code

- Terraform
- Helm charts

Works for:
- SaaS
- BYOC
- On-Prem

---

## Observability (Phase-1 Scope)

- Prometheus (metrics)
- OpenTelemetry (hooks only)
- Centralized logging (ELK / OpenSearch stack)

Runtime-to-architecture observability comes in later phases.

---

## On-Prem Compatibility (Hard Requirement)

- All dependencies self-hostable
- No cloud-managed-only services
- Externalized configuration
- Customer-managed secrets allowed
- Air-gapped deployments supported

---

## Explicit Non-Choices (Locked Out)

- Java-based backend
- Serverless-first architecture
- Vendor-locked graph services
- UI-only modeling
- AI-generated architecture (Phase-1)

---

## Upgrade & Evolution Path

- Modular monolith → services (later)
- Neo4j abstraction allows future graph replacement
- Messaging adapters allow infra swap
- Frontend component library introduced later
- .NET allows long-term performance tuning

---

## What This Stack Enables

- Fast onboarding for .NET teams
- Strong enterprise adoption
- On-Prem + Cloud parity
- High-performance graph queries
- Clean, testable architecture
- Long-term maintainability

---

## Status

This document defines the **authoritative .NET / C# technology stack and architecture choices**.
All implementation must conform unless explicitly reopened.
