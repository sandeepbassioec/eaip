# API Gateway & External Interaction Flows

## Purpose

This document defines:
- How external clients interact with EAIP
- The role of the API Gateway
- Authentication and authorization boundaries
- Interaction flows for UI, integrations, and events

It establishes a **single, governed entry and exit layer** for the platform.

---

## Guiding Principles

1. All external traffic flows through the API Gateway
2. No client accesses bounded contexts directly
3. Authentication and authorization are enforced at the edge
4. APIs are versioned and backward-compatible
5. Event-driven communication is preferred over synchronous coupling

---

## 1. API Gateway Responsibilities

The API Gateway acts as the **system edge**.

### Core Responsibilities
- Request routing
- Authentication
- Authorization
- Rate limiting
- Throttling
- API versioning
- Request validation
- Response normalization

---

## 2. Client Types

### 2.1 Human Clients
- Web UI
- Admin consoles

### 2.2 System Clients
- Client applications
- CI/CD pipelines
- External architecture tools

### 2.3 Integration Clients
- Webhook endpoints
- Message queues
- Event subscribers

---

## 3. Authentication Model

### Supported Authentication Types
- OAuth 2.0 / OIDC (users)
- API keys (system integrations)
- Short-lived tokens (automation)

### Authentication Rules
- All requests must be authenticated
- Tokens are workspace-scoped
- Tokens carry role and permission claims

---

## 4. Authorization Model

Authorization is enforced at **multiple levels**:

### Levels
1. Workspace access
2. Role-based permissions
3. Artifact-level permissions (ADR, Diagram, Application)

### Authorization Rules
- Read and write permissions are distinct
- Approval actions require elevated privileges
- Integration users are restricted to declared scopes

---

## 5. API Versioning Strategy

- All APIs are versioned (e.g., `/v1/`)
- Breaking changes require a new major version
- Multiple versions may coexist
- Deprecation policies are explicit and time-bound

---

## 6. External Interaction Flows

### 6.1 Web UI Interaction Flow

Browser
→ API Gateway
→ Application Layer
→ Domain Context
→ Event Published

**Characteristics**
- Stateless requests
- Token-based authentication
- Optimistic UI updates
- Event-driven refresh

---

### 6.2 System-to-System API Flow

Client System
→ API Gateway
→ Application Service
→ Domain Aggregate
→ Domain Event


**Use Cases**
- Application registration
- ADR creation
- Diagram ingestion
- Roadmap updates

---

### 6.3 Outbound Event (Webhook) Flow

Domain Event
→ Event Exchange Context
→ Subscription Resolution
→ Webhook Delivery
→ Client Endpoint

**Key Properties**
- HMAC-signed payloads
- Retry with backoff
- Delivery auditing
- Dead-letter handling

---

### 6.4 Inbound Event Flow (Client → EAIP)

Client System
→ Inbound Event Endpoint
→ Event Validation
→ Event Exchange Context
→ Internal Event Published

**Rules**
- Schema validation is mandatory
- Events are workspace-scoped
- Invalid events are rejected and audited

---

## 7. Rate Limiting & Throttling

### Policies
- Per-workspace limits
- Per-token limits
- Burst handling

### Behavior
- Throttled requests return explicit errors
- Limits are configurable per subscription tier

---

## 8. Error Handling & Responses

### Error Categories
- Authentication errors
- Authorization errors
- Validation errors
- Rate limit errors
- Internal processing errors

### Error Principles
- No internal details leaked
- Correlation IDs returned
- Errors are logged and auditable

---

## 9. Security Boundaries

### Enforced At Gateway
- Authentication
- Authorization
- Input validation
- Request size limits

### Enforced Downstream
- Domain invariants
- Policy checks
- Audit recording

---

## 10. Observability at the Edge

### Captured Metrics
- Request latency
- Error rates
- Throttle counts
- Token usage

### Logging
- Correlation IDs
- Actor identity
- Request outcome

---

## 11. Forbidden Patterns

- Direct access to bounded context services
- Bypassing gateway authentication
- Long-running synchronous requests
- Stateful sessions at the gateway

---

## Status

This document defines the **authoritative external interaction contract** for EAIP.

All clients, integrations, and tools must interact with the platform exclusively through the API Gateway.

