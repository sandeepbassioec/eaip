
**Bounded contexts are defined only in the Domain Plane.**

---

## Bounded Contexts Overview

### 1. Identity & Access Context

**Responsibility**
- User identities
- Roles and permissions
- Workspace isolation

**Owns**
- User
- Role
- Permission
- Policy
- WorkspaceMembership

**Does Not Know**
- Applications
- ADRs
- Architecture models

---

### 2. Workspace Context

**Responsibility**
- Tenant lifecycle
- Organization metadata
- Compliance configuration
- Default cloud preferences

**Owns**
- Workspace
- OrganizationProfile
- ComplianceProfile

**Publishes Events**
- Workspace.Created
- Workspace.Updated

---

### 3. Application Portfolio Context

**Responsibility**
- Application registry
- Business unit ownership
- Application lifecycle

**Owns**
- Application
- BusinessUnit
- Domain
- LifecycleState

**Key Rule**
- Application is an **aggregate root**

**Publishes Events**
- Application.Created
- Application.Updated
- Application.Sunset

---

### 4. Semantic Tagging Context

**Responsibility**
- Typed and weighted tags
- Cross-cutting classification

**Owns**
- Tag
- TagType
- TagAssignment

**Design Note**
- This context classifies other contexts but owns no business processes

---

### 5. Architecture Decision Record (ADR) Context

**Responsibility**
- Capture and govern architectural decisions
- Decision lifecycle and approvals
- Versioning and auditability

**Owns**
- ADR
- ADRVersion
- DecisionStatus
- Approval

**Key Rule**
- No architecture artifact exists without an ADR

---

### 6. Architecture Modeling Context

**Responsibility**
- Architecture diagrams and models
- Typed nodes and relationships
- Versioning and diffing

**Owns**
- Diagram
- DiagramVersion
- Node
- Edge
- Relationship

**Supported Diagram Types**
- C4
- HLD / LLD
- Integration
- ER
- Deployment

---

### 7. Cloud Capability Context

**Responsibility**
- Canonical cloud capability definitions
- Cloud provider mappings
- Feature parity awareness

**Owns**
- Capability
- CapabilityProfile
- CloudProviderMapping

**Design Rule**
- No direct dependency on cloud provider SDKs

---

### 8. Roadmap & Transformation Context

**Responsibility**
- Current vs target architecture
- Migration planning
- Dependency and risk tracking

**Owns**
- Roadmap
- Milestone
- TransformationPlan
- Risk

---

### 9. Event Exchange Context

**Responsibility**
- Event catalog and schemas
- Subscriptions and delivery
- Webhook and queue-based integrations

**Owns**
- EventType
- EventSchema
- Subscription
- DeliveryEndpoint

**Design Rule**
- Supports bi-directional communication (Platform ↔ Client)

---

### 10. Activity & Audit Context

**Responsibility**
- System activity timeline
- Audit and compliance records
- Traceability across contexts

**Owns**
- Activity
- AuditRecord
- Actor

**Consumes Events From**
- All other bounded contexts

---

## Context Interaction Rules

### Allowed
- Event-based communication between contexts
- Read-only queries for reporting

### Forbidden
- Direct database access across contexts
- Shared aggregates
- Circular dependencies

---

## Ownership & Team Alignment

Each bounded context must have:
- A clear owning team
- Independent release capability
- Well-defined public interfaces (APIs or events)

---

## Change Policy

- Changes to bounded contexts **must update this document**
- New contexts require explicit justification
- Context merges or splits must be documented

---

## Status

This document is **authoritative** and **actively maintained**.

