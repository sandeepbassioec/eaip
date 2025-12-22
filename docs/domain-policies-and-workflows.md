# Domain Invariants, Policies & Workflows

## Purpose

This document defines the **behavioral rules** of the Enterprise Architecture Intelligence Platform (EAIP).

It captures:
- Domain invariants (hard rules)
- Policies (conditional business rules)
- Workflows (event-driven orchestration)

This document bridges the gap between **domain models** and **system architecture**.

---

## Definitions

### Invariant
A rule that **must always hold true**.  
Violation = system inconsistency.

### Policy
A conditional rule that **guides decisions**.  
Policies may change over time.

### Workflow
An ordered or event-driven sequence of actions across one or more contexts.

---

## 1. Identity & Access Context

### Invariants
- A disabled user cannot authenticate or invoke APIs
- A user must belong to at least one workspace
- Permissions are always workspace-scoped

### Policies
- Users with Architect role may approve ADRs
- Workspace Admins may delegate roles
- External Integration Users are API-only

### Workflows
- **User Onboarding**
  1. User created
  2. Workspace membership assigned
  3. Roles granted
  4. Access activated

---

## 2. Workspace Context

### Invariants
- Workspace ID is immutable
- Compliance flags cannot be removed once enabled

### Policies
- Compliance-enabled workspaces require audit logging
- Default cloud preference applies unless overridden

### Workflows
- **Workspace Creation**
  1. Workspace created
  2. Organization profile initialized
  3. Compliance profile applied
  4. Workspace.Created event published

---

## 3. Application Portfolio Context

### Invariants
- An application belongs to exactly one business unit
- Lifecycle transitions must follow defined states

### Policies
- Tier-1 applications require approved ADRs
- Sunset applications cannot accept new integrations

### Workflows
- **Application Registration**
  1. Application metadata validated
  2. Application created
  3. Default lifecycle state assigned
  4. Application.Created event published

---

## 4. Semantic Tagging Context

### Invariants
- Tag types are controlled and predefined
- Tag weights must be within allowed range

### Policies
- Risk tags require justification
- Compliance tags propagate to linked artifacts

### Workflows
- **Tag Assignment**
  1. Target entity validated
  2. Tag assigned
  3. Tag.Assigned event published

---

## 5. Architecture Decision Record (ADR) Context

### Invariants
- Approved ADRs are immutable
- Superseded ADRs must reference a successor

### Policies
- Certain ADR types require multi-approver review
- High-impact ADRs require architecture board approval

### Workflows
- **ADR Approval**
  1. ADR submitted for review
  2. Reviewers notified
  3. Approval recorded
  4. ADR.Approved event published

---

## 6. Architecture Modeling Context

### Invariants
- Diagrams must belong to a valid application
- Only published diagrams may be referenced externally

### Policies
- Diagram publication requires an approved ADR
- Target-state diagrams require roadmap linkage

### Workflows
- **Diagram Publication**
  1. Diagram validated
  2. ADR linkage verified
  3. Diagram published
  4. Diagram.Published event emitted

---

## 7. Cloud Capability Context

### Invariants
- Capabilities are provider-independent
- Canonical definitions cannot be overridden

### Policies
- Capability parity warnings must be disclosed
- Unsupported mappings require explicit acknowledgment

### Workflows
- **Capability Mapping**
  1. Capability defined
  2. Cloud provider mapping added
  3. Parity level assessed
  4. Capability.Mapped event published

---

## 8. Roadmap & Transformation Context

### Invariants
- Roadmaps must reference a valid application
- Milestones must be sequential

### Policies
- High-risk transformations require mitigation plans
- Target-state architectures must align with ADRs

### Workflows
- **Roadmap Definition**
  1. Current state captured
  2. Target state defined
  3. Migration steps added
  4. Roadmap.Created event published

---

## 9. Event Exchange Context

### Invariants
- Subscriptions are workspace-scoped
- Event schemas are immutable per version

### Policies
- Webhook delivery is default
- Failed deliveries must be retried with backoff

### Workflows
- **Event Delivery**
  1. Event received
  2. Subscriptions resolved
  3. Payload delivered
  4. Delivery result recorded

---

## 10. Activity & Audit Context

### Invariants
- Audit records are append-only
- Audit data cannot be modified or deleted

### Policies
- Compliance-enabled workspaces require extended retention
- Sensitive actions require higher audit detail

### Workflows
- **Audit Recording**
  1. Domain event received
  2. Audit record created
  3. Activity timeline updated

---

## Cross-Context Workflow Rules

- Workflows communicate via events only
- No workflow may synchronously control another context
- Failure handling must be explicit and auditable

---

## Status

This document defines the **behavioral contract** of the system and must be updated whenever:
- A new invariant is introduced
- A policy changes
- A workflow is added or modified

