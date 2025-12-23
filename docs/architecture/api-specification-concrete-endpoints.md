# API Specification – Concrete Endpoints & Contracts

## Purpose

This document defines the **concrete, build-ready REST API specification**
for the **Enterprise Architecture Visibility & Intelligence Platform (EAVIP)**.

It is the **engineering contract** for backend teams and ensures:
- Predictable integrations
- Strong governance enforcement
- Safe graph access
- Versioned, enterprise-grade APIs

---

## Core Rules (Non-Negotiable)

1. REST APIs are used for **commands and reads**
2. No raw graph query language is exposed
3. Every request is tenant-scoped
4. Time context is mandatory
5. APIs are versioned from day one
6. Every write emits an immutable event

---

## API Conventions

### Base URL
/api/v1


### Mandatory Headers
X-Tenant-Id: <uuid>
X-User-Id: <uuid | service-id>
X-Time-Context: now | <timestamp>
Authorization: Bearer <token>


Requests missing these headers must fail immediately.

---

## Identity & Context APIs

### Get Current Execution Context
GET /api/v1/context

**Response**
```json
{
  "tenantId": "uuid",
  "userId": "uuid",
  "roles": ["Architect", "Viewer"],
  "timeContext": "now"
}
```
---
Enterprise Structure APIs
Create Organization (Command)

Enterprise Structure APIs
Create Organization (Command)

Request
{
  "name": "Payments Division",
  "owner": "Finance"
}

Behavior

Creates a proposal if governance is enabled

Emits OrganizationProposed event
---
List Organizations (Read)
GET /api/v1/organizations
---

Application & Component APIs
Create Application
POST /api/v1/applications
{
  "organizationId": "uuid",
  "name": "Payments API",
  "criticality": "HIGH",
  "lifecycle": "ACTIVE"
}
---
Create Component
POST /api/v1/components
{
  "applicationId": "uuid",
  "name": "Transaction Processor",
  "type": "SERVICE"
}
---
Dependency APIs (Critical)
Propose Dependency
POST /api/v1/dependencies
{
  "from": { "type": "Component", "id": "uuid" },
  "to": { "type": "Component", "id": "uuid" },
  "relationship": "CALLS",
  "protocol": "HTTP",
  "dataSensitivity": "PII"
}

Rules

Does not mutate the graph directly

Enters governance workflow

Emits DependencyProposed
---
Graph Query APIs (Read-Only)
Impact Analysis

GET /api/v1/graph/impact
Query Parameters
nodeId=<uuid>
depth=3
direction=downstream | upstream

Response
{
  "rootNode": "uuid",
  "nodes": [],
  "relationships": []
}

Guards

Depth limited
Node count capped
Tenant scoped
---

Time-Based Snapshot Query
GET /api/v1/graph/snapshot?at=2024-12-31T00:00:00Z
---
Document & ADR APIs
Attach Document
POST /api/v1/documents
{
  "entityType": "Application",
  "entityId": "uuid",
  "documentType": "ADR",
  "format": "markdown",
  "content": "..."
}
---

Governance APIs
Approve or Reject Proposal
POST /api/v1/governance/approvals
{
  "proposalId": "uuid",
  "decision": "APPROVED | REJECTED",
  "comment": "Reviewed and approved"
}
---

Event Subscription APIs
Register Webhook
POST /api/v1/subscriptions/webhooks
{
  "eventTypes": [
    "DependencyApproved",
    "DriftDetected",
    "PolicyViolated"
  ],
  "endpoint": "https://client.example.com/webhook"
}
---
Error Model (Uniform)
{
  "errorCode": "GOVERNANCE_VIOLATION",
  "message": "Dependency violates policy XYZ",
  "correlationId": "uuid"
}
---
Versioning Strategy
* /api/v1 is immutable
* Breaking changes require /api/v2
* Old versions supported with deprecation windows
* Events are versioned independently
---
Security & Rate Limiting
* OAuth2 / OIDC authentication
* Scoped access tokens
* Tenant-based rate limits
* Write APIs more restrictive than read APIs
---
What This Specification Avoids

* Over-fetching
* Unsafe graph traversal
* Vendor lock-in
* Ambiguous contracts
* Hidden governance bypasses
---
Outcome
With this API specification:
*  Backend teams can implement immediately
*  Frontend teams know exact contracts
*  Integrations remain stable and safe
*  Governance is enforced at boundaries
---
Status

This document defines the authoritative concrete API contract for EAVIP.

All backend implementation must conform to this specification.
