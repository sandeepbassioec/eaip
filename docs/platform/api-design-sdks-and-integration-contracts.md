# API Design, SDKs & External Integration Contracts

## Purpose

This document defines the **external and internal API strategy** for the
Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It ensures:
- Safe access to the Enterprise Graph
- Clear contracts for integrations, plugins, and partners
- Backward compatibility at enterprise scale
- Governance, security, and tenancy enforced by design

APIs are **capability boundaries**, not data pipes.

---

## Core Principles

1. **Graph truth remains internal**
2. **APIs expose intent, not storage**
3. **Read-heavy, write-guarded**
4. **Explicit versioning**
5. **Contracts > convenience**
6. **Zero implicit trust**

---

## 1. API Surface Overview

EAVIP exposes **three API surfaces**:

| Surface | Audience | Purpose |
|-------|----------|---------|
| Public APIs | Customers & integrators | Read, propose, subscribe |
| Partner / Plugin APIs | Extensions | Ingest, analyze, visualize |
| Internal APIs | Platform services | Strongly-typed, trusted |

> **Rule:** Internal APIs are never exposed externally.

---

## 2. API Paradigms (Hybrid by Design)

### 2.1 REST APIs (Authoritative for Mutations)

Used for:
- Commands
- Proposals
- Approvals
- Lifecycle actions

Characteristics:
- Explicit endpoints
- Idempotent where possible
- Strong validation
- Clear error semantics

---

### 2.2 Graph Query APIs (Read-Only)

Used for:
- Traversal
- Impact analysis
- Diagram generation
- Exploration

Characteristics:
- Read-only
- Bounded traversal depth
- Role-filtered
- Time-aware

> **No raw graph DB exposure. Ever.**

---

### 2.3 Event APIs (Asynchronous)

Used for:
- Webhooks
- Queues
- Event subscriptions

Characteristics:
- Immutable events
- Versioned schemas
- At-least-once delivery (configurable)

---

## 3. Tenancy, Identity & Context (MANDATORY)

Every API request carries:
- TenantId
- OrganizationId (optional, scoped)
- UserId / ServiceId
- Roles
- TimeContext (as-is / to-be / historical)

Requests without context **fail fast**.

---

## 4. Public API Capabilities

### 4.1 Read APIs
- Browse enterprise / org / app graph
- Retrieve auto-generated diagrams
- Query dependencies & data flows
- Fetch documents & ADRs

---

### 4.2 Propose APIs (Write, Guarded)
- Propose architecture changes
- Propose dependencies
- Propose ADRs
- Propose risk acceptance

All proposals:
- Are non-destructive
- Enter review workflows
- Produce audit events

---

### 4.3 Approval APIs
- Approve / reject proposals
- Record rationale
- Time-bound decisions

Approval rights are **role-restricted**.

---

## 5. Graph Query Model (Safe Traversal)

### 5.1 Query Constraints
- Max depth
- Max node count
- Allowed relationship types
- Time slice required

Prevents:
- Graph explosions
- Data exfiltration
- Performance abuse

---

### 5.2 Example Queries (Conceptual)
- “Show all outbound dependencies of App X”
- “What breaks if Component Y changes?”
- “Show cross-org data flows in Q3”

---

## 6. SDK Strategy (Enterprise-Friendly)

### 6.1 Supported SDKs (Phase-wise)

| Language | Audience |
|--------|----------|
| TypeScript / JS | Frontend, tooling |
| .NET | Enterprise backends |
| Java | Enterprise backends |
| Python | Automation, analytics |

SDKs provide:
- Strong typing
- Pagination & retries
- Context propagation
- Auth helpers

---

### 6.2 SDK Design Rules
- SDKs never hide failures
- SDKs never bypass governance
- SDKs are thin wrappers over APIs
- Versioned independently

---

## 7. Webhook Contracts

### 7.1 Event Categories
- GraphChanged
- DependencyProposed
- DriftDetected
- PolicyViolated
- DocumentApproved

---

### 7.2 Webhook Semantics
- Signed payloads
- mTLS optional
- Retry with backoff
- DLQ support (adapter-based)

---

## 8. Queue-Based Integration Contracts

### 8.1 Supported Models
- Kafka
- RabbitMQ
- ActiveMQ / IBM MQ
- Cloud equivalents

### 8.2 Contract Rules
- Schema-first (Avro / JSON Schema)
- Versioned events
- Backward-compatible evolution

---

## 9. Partner & Plugin Contracts

### 9.1 Partner API Scope
- Read-only graph access (scoped)
- Ingestion endpoints
- Event subscriptions

---

### 9.2 What Partners Cannot Do
- Mutate core graph directly
- Change ownership
- Bypass approvals
- Disable governance

---

## 10. Versioning & Compatibility (CRITICAL)

### 10.1 API Versioning
- URI or header-based
- Long deprecation windows
- Explicit breaking-change policy

---

### 10.2 Event Schema Evolution
- Additive changes preferred
- Breaking changes require new topic/event
- Old consumers supported during transition

---

## 11. Error Handling & Diagnostics

- Clear error codes
- Human-readable messages
- Correlation IDs
- Audit events for failures

No silent failures.

---

## 12. Rate Limiting & Abuse Protection

- Tenant-scoped limits
- Burst + sustained limits
- Read vs write quotas
- Back-pressure signals

---

## 13. Security Controls

- OAuth2 / OIDC
- mTLS (optional)
- Scoped tokens
- Secret rotation support

---

## 14. What This API Model Avoids

- Raw database access
- Overpowered admin APIs
- Unversioned contracts
- “Just query everything” endpoints
- Tight coupling to UI needs

---

## Outcome

With this model:
- Integrations are safe and predictable
- Governance is enforced at boundaries
- SDKs feel natural to enterprises
- Partners can innovate without risk
- The Enterprise Graph remains protected

---

## Status

This document defines the **authoritative API, SDK, and integration contract model**.

All external access to EAVIP **must conform** to this design.
