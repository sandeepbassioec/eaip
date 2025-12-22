# High-Level Architecture (Logical & Physical)

## Purpose

This document defines the **high-level architecture** of the Enterprise Architecture Intelligence Platform (EAIP).

It translates:
- Domain models
- Bounded contexts
- Policies and workflows

into a **logical and physical system structure** that supports:
- SaaS delivery
- Cloud independence
- Scalability
- Security
- Event-driven collaboration

This document intentionally avoids:
- Programming languages
- Frameworks
- Cloud-vendor-specific implementations

---

## Architectural Goals

- Clear separation of concerns
- Independent evolution of bounded contexts
- Event-first communication
- Support for SaaS and BYOC deployment
- No single point of failure
- Auditability and traceability by design

---

## 1. Logical Architecture

### 1.1 Architectural Layers

The system is logically divided into the following layers:

Client Layer
API & Interaction Layer
Application Layer
Domain Layer
Infrastructure Abstraction Layer


---

### 1.2 Client Layer

**Responsibilities**
- User interaction
- Visualization of diagrams and roadmaps
- Subscription and integration management

**Clients**
- Web UI
- External systems (via webhooks / APIs)
- Automation tools

**Key Characteristics**
- Stateless
- Token-based authentication
- No direct domain logic

---

### 1.3 API & Interaction Layer

**Responsibilities**
- Request validation
- Authentication and authorization
- Routing to application services
- Rate limiting and throttling

**Exposes**
- Public APIs per bounded context
- Integration endpoints
- Event ingestion endpoints

**Key Characteristics**
- Context-aware routing
- Policy enforcement
- No persistence logic

---

### 1.4 Application Layer

**Responsibilities**
- Orchestration of workflows
- Command and query handling
- Policy evaluation
- Cross-context coordination via events

**Characteristics**
- Stateless
- Uses domain models
- Publishes and consumes events
- No direct infrastructure dependencies

---

### 1.5 Domain Layer

**Responsibilities**
- Core business logic
- Aggregates and invariants
- Domain events

**Characteristics**
- Pure domain logic
- No infrastructure awareness
- Enforces consistency boundaries

---

### 1.6 Infrastructure Abstraction Layer

**Responsibilities**
- Messaging
- Persistence
- Search
- Storage
- Observability

**Key Rule**
- Domain and application layers depend only on abstractions
- Implementations are replaceable per cloud or environment

---

## 2. Physical Architecture

### 2.1 Deployment Units

Each bounded context may be deployed as:
- An independent service
- A modular component within a service (initially)

Deployment units are **context-aligned**, not layer-aligned.

---

### 2.2 Control Plane vs Data Plane

#### Control Plane
- User management
- Architecture modeling
- ADR governance
- Event routing

#### Data Plane
- Client-specific integrations
- Webhook delivery
- Optional BYOC resources

This separation supports:
- SaaS scalability
- Regulatory isolation
- Hybrid deployment models

---

### 2.3 Event Backbone

All inter-context and external communication flows through an **event backbone**.

**Event Types**
- Domain events
- Integration events
- Audit events

**Characteristics**
- Asynchronous
- Durable
- Replayable
- Auditable

---

### 2.4 Persistence Model (Logical)

| Data Type | Logical Store |
|--------|--------------|
| Metadata (Apps, ADRs) | Relational |
| Relationships (Dependencies) | Graph |
| Diagrams & Versions | Object Storage |
| Search & Insights | Indexed Store |
| Audit Logs | Append-only Store |

---

### 2.5 Security Architecture

**Principles**
- Zero trust
- Least privilege
- Strong tenant isolation

**Enforced At**
- API boundaries
- Event delivery
- Subscription endpoints

**Security Domains**
- Platform
- Workspace
- Integration

---

## 3. Interaction Patterns

### 3.1 Command Flow

Client → API Layer → Application Service → Domain Aggregate → Event Published

---

### 3.2 Query Flow

Client → API Layer → Read Model → Response

---

### 3.3 Event Flow (Internal)

Context A → Domain Event → Event Backbone → Context B

---

### 3.4 Event Flow (External)

Domain Event → Event Exchange → Webhook / Queue → Client System

---

## 4. Scalability Model

- Horizontal scaling per deployment unit
- Stateless services
- Event-driven load distribution
- Independent scaling of read and write paths

---

## 5. Failure & Resilience Strategy

- Retry with backoff
- Dead-letter handling
- Graceful degradation
- Partial failure isolation via bounded contexts

---

## 6. Deployment Models Supported

1. Fully Managed SaaS
2. Bring Your Own Cloud (BYOC)
3. Hybrid Control Plane / Data Plane

Each model uses the same logical architecture with different physical realizations.

---

## 7. Architectural Constraints

- No synchronous cross-context business logic
- No shared databases across contexts
- No cloud-provider lock-in at domain level
- All changes must be traceable via events

---

## Status

This document defines the **authoritative high-level architecture** of EAIP.

All detailed designs, implementations, and deployments must conform to this structure.

