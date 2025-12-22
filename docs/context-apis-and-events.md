# Context APIs & Event Contracts

## Purpose

This document defines the **public-facing APIs and event contracts** for each bounded context in the Enterprise Architecture Intelligence Platform (EAIP).

It establishes:
- How bounded contexts communicate
- What each context exposes
- Which events are published and consumed
- Clear ownership and dependency rules

This document is **technology-agnostic** and intentionally avoids implementation details.

---

## Guiding Rules

1. Each bounded context exposes **explicit APIs**
2. Cross-context communication is **event-driven first**
3. No context directly accesses another context’s data store
4. Events are immutable, versioned, and auditable
5. Read models may query other contexts **read-only**

---

## 1. Identity & Access Context

### Public APIs
- CreateUser
- DisableUser
- AssignRole
- RevokeRole
- GrantPermission
- RevokePermission

### Published Events
- User.Created
- User.Disabled
- Role.Assigned
- Role.Revoked
- Permission.Granted
- Permission.Revoked

### Consumed Events
- Workspace.Created (from Workspace Context)

---

## 2. Workspace Context

### Public APIs
- CreateWorkspace
- UpdateWorkspaceProfile
- UpdateComplianceSettings
- SetDefaultCloudPreference

### Published Events
- Workspace.Created
- Workspace.Updated
- Workspace.Deactivated

### Consumed Events
- None

---

## 3. Application Portfolio Context

### Public APIs
- RegisterApplication
- UpdateApplicationMetadata
- ChangeLifecycleState
- AssignBusinessUnit

### Published Events
- Application.Created
- Application.Updated
- Application.Sunset

### Consumed Events
- Workspace.Created
- Tag.Assigned
- Tag.Removed

---

## 4. Semantic Tagging Context

### Public APIs
- CreateTag
- AssignTag
- RemoveTag
- UpdateTagWeight

### Published Events
- Tag.Created
- Tag.Assigned
- Tag.Removed
- Tag.Updated

### Consumed Events
- Application.Created
- ADR.Created
- Diagram.Published

---

## 5. Architecture Decision Record (ADR) Context

### Public APIs
- CreateADR
- UpdateADR
- SubmitForReview
- ApproveADR
- SupersedeADR
- DeprecateADR

### Published Events
- ADR.Created
- ADR.Submitted
- ADR.Approved
- ADR.Superseded
- ADR.Deprecated

### Consumed Events
- Application.Created
- Workspace.Updated

---

## 6. Architecture Modeling Context

### Public APIs
- CreateDiagram
- UpdateDiagram
- PublishDiagram
- CreateDiagramVersion
- CompareDiagramVersions

### Published Events
- Diagram.Created
- Diagram.Updated
- Diagram.Published
- Diagram.Versioned

### Consumed Events
- ADR.Approved
- Application.Updated

---

## 7. Cloud Capability Context

### Public APIs
- DefineCapability
- MapCapabilityToCloud
- UpdateCapabilityProfile
- ValidateCapabilityParity

### Published Events
- Capability.Created
- Capability.Mapped
- Capability.Updated

### Consumed Events
- Workspace.Updated

---

## 8. Roadmap & Transformation Context

### Public APIs
- CreateRoadmap
- DefineTargetArchitecture
- AddMigrationStep
- AssessTransformationRisk

### Published Events
- Roadmap.Created
- Roadmap.Updated
- MigrationStep.Added
- Risk.Identified

### Consumed Events
- Application.Updated
- Diagram.Published
- ADR.Approved

---

## 9. Event Exchange Context

### Public APIs
- RegisterEventType
- CreateSubscription
- UpdateSubscription
- DisableSubscription
- PublishExternalEvent

### Published Events
- Subscription.Created
- Subscription.Disabled
- ExternalEvent.Received
- Event.Delivered
- Event.Failed

### Consumed Events
- All domain events (for routing and delivery)

---

## 10. Activity & Audit Context

### Public APIs
- QueryActivityTimeline
- QueryAuditRecords

### Published Events
- Audit.Recorded

### Consumed Events
- All domain events

---

## Event Contract Standards

### Event Structure

EventId
EventType
EventVersion
WorkspaceId
OccurredAt
Actor
Payload
CorrelationId


---

## Event Versioning Rules

- Events are immutable
- Breaking changes require a new version
- Consumers must explicitly opt into newer versions

---

## Cross-Context Dependency Matrix

| Context | Depends On |
|------|-----------|
| Identity | Workspace |
| Application | Workspace, Tagging |
| ADR | Application |
| Modeling | ADR, Application |
| Roadmap | ADR, Modeling |
| Event Exchange | All |
| Audit | All |

---

## Forbidden Patterns

- Synchronous calls across contexts for business logic
- Shared domain models
- Context-specific rules leaking outside boundaries

---

## Status

This document defines the **official communication contracts** between bounded contexts and must be updated whenever:
- A new API is added
- An event is introduced or changed
- A dependency is modified

