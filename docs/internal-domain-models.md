# Internal Domain Models (Bounded Contexts)

## Purpose

This document defines the **internal domain models** for each bounded context in the Enterprise Architecture Intelligence Platform (EAIP).

It describes:
- Core domain entities
- Aggregate roots
- Value objects
- Business invariants

This document intentionally avoids:
- Technical implementation details
- Persistence models
- Framework or language decisions

---

## Modeling Rules

1. Each bounded context owns its domain models exclusively
2. Aggregates enforce consistency boundaries
3. Cross-context references are by **ID only**
4. Invariants must be enforced inside aggregates
5. Domain models do not depend on infrastructure

---

## 1. Identity & Access Context

### Aggregate Root: User

**Entities**
- User
- WorkspaceMembership

**Value Objects**
- UserId
- Email
- RoleId
- PermissionId

**Invariants**
- A user must belong to at least one workspace
- A disabled user cannot authenticate
- Roles and permissions are workspace-scoped

---

## 2. Workspace Context

### Aggregate Root: Workspace

**Entities**
- Workspace
- OrganizationProfile
- ComplianceProfile

**Value Objects**
- WorkspaceId
- IndustryType
- CloudPreference

**Invariants**
- Workspace ID is immutable
- Compliance flags cannot be removed once enforced
- Each workspace has exactly one organization profile

---

## 3. Application Portfolio Context

### Aggregate Root: Application

**Entities**
- Application
- BusinessUnit
- Domain

**Value Objects**
- ApplicationId
- LifecycleState
- CriticalityLevel

**Invariants**
- Application ID is immutable
- An application must belong to exactly one business unit
- Lifecycle transitions must follow defined states

---

## 4. Semantic Tagging Context

### Aggregate Root: Tag

**Entities**
- Tag
- TagAssignment

**Value Objects**
- TagId
- TagType
- Weight

**Invariants**
- Tag types are predefined and controlled
- Tag assignments must reference valid target IDs
- Weight values must be within allowed range

---

## 5. Architecture Decision Record (ADR) Context

### Aggregate Root: ADR

**Entities**
- ADR
- ADRVersion
- Approval

**Value Objects**
- ADRId
- DecisionStatus
- ApproverId

**Invariants**
- An ADR must have at least one version
- Approved ADRs are immutable
- Superseding an ADR requires justification

---

## 6. Architecture Modeling Context

### Aggregate Root: Diagram

**Entities**
- Diagram
- DiagramVersion
- Node
- Edge

**Value Objects**
- DiagramId
- NodeType
- RelationshipType

**Invariants**
- A diagram must belong to exactly one application
- Only published diagrams are referenceable
- Nodes and edges must conform to diagram type rules

---

## 7. Cloud Capability Context

### Aggregate Root: Capability

**Entities**
- Capability
- CapabilityProfile
- CloudProviderMapping

**Value Objects**
- CapabilityId
- CapabilityType
- ParityLevel

**Invariants**
- Capabilities are defined independently of providers
- Provider mappings cannot override canonical definitions
- Parity levels must be explicitly declared

---

## 8. Roadmap & Transformation Context

### Aggregate Root: Roadmap

**Entities**
- Roadmap
- Milestone
- TransformationPlan
- Risk

**Value Objects**
- RoadmapId
- RiskLevel
- TargetState

**Invariants**
- A roadmap must reference a valid application
- Milestones must be sequential
- Risks must be explicitly acknowledged or m
