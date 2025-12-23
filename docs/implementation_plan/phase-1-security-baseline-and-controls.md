# Phase 1 Security Baseline & Controls

## Purpose

This document defines the authoritative security baseline and mandatory controls
for Phase 1 (MVP Execution) of the Enterprise Architecture Visibility &
Intelligence Platform (EAVIP).

It ensures that:
- Security is built-in, not retrofitted
- On-Prem and Cloud deployments share the same security posture
- Tenant isolation is absolute
- Governance and auditability are non-negotiable

This is the security execution contract for Phase 1.

---

## Security Principles (Locked)

1. Secure by default, configurable by exception
2. Tenant isolation is absolute
3. No implicit trust between components
4. Least privilege everywhere
5. Security controls must be auditable
6. Fail closed, not open

---

## Identity & Authentication

### Requirements

- OAuth2 / OpenID Connect mandatory
- External Identity Providers supported
- JWT-based access tokens
- Token expiry strictly enforced

### Controls

- No anonymous access
- No long-lived tokens
- Token audience and issuer validation required
- Clock-skew limits enforced

---

## Authorization & Access Control

### Model

- Role-Based Access Control (RBAC)
- Policy-based authorization on top of RBAC
- Tenant context mandatory on every request

### Controls

- Authorization enforced at API boundary
- Authorization re-checked at application layer
- No client-side trust for permissions
- Explicit deny overrides implicit allow

---

## Tenant Isolation

### Requirements

- Tenant identifier mandatory in every request
- Data access always scoped to tenant
- Cross-tenant access is impossible by design

### Controls

- Tenant context injected via middleware
- Database queries always tenant-scoped
- Graph queries always tenant-filtered
- Background workers enforce tenant boundaries

---

## API Security

### Controls

- HTTPS required everywhere
- Strong TLS configuration
- Rate limiting per tenant
- Input validation on all endpoints
- Output shaping to prevent data leakage

---

## Data Protection

### At Rest

- Database encryption enabled
- Disk-level encryption mandatory
- Secrets never stored in code or config files

### In Transit

- TLS for all internal and external communication
- Mutual TLS supported for on-prem integrations
- Certificate rotation supported

---

## Secrets Management

### Requirements

- External secrets store mandatory
- No secrets in source control
- No secrets in container images

### Supported Options

- Cloud secrets managers
- On-Prem vault solutions
- Environment-based injection

---

## Audit & Traceability

### Requirements

- All state-changing actions audited
- Governance decisions fully traceable
- Audit logs are append-only

### Controls

- Actor, timestamp, intent, and outcome recorded
- Audit records are immutable
- Audit access is read-only

---

## Background Processing Security

### Controls

- Workers authenticate using service identities
- Workers have minimal permissions
- Idempotency enforced to prevent replay attacks

---

## Dependency & Supply Chain Security

### Controls

- Dependency scanning enabled
- Known vulnerable dependencies blocked
- Container images scanned
- Base images pinned and reviewed

---

## On-Prem Specific Security Controls

### Requirements

- Works in restricted networks
- Supports customer-managed certificates
- Supports customer-managed identity providers

### Controls

- No hard dependency on cloud-only services
- All external calls configurable or disableable
- Webhooks secured via shared secret or mTLS

---

## Explicit Non-Goals (Phase 1)

- Zero-trust runtime enforcement across workloads
- Automated threat detection
- AI-driven security analysis
- Runtime behavior anomaly detection

These are deferred to later phases.

---

## Security Review & Validation

- Security review required before pilot onboarding
- Penetration testing recommended before production
- Misconfiguration checks automated

---

## Outcome

With this security baseline:
- Phase-1 deployments are enterprise-safe
- Trust is established early
- Security debt is avoided
- Cloud and on-prem parity is maintained

---

## Status

This document defines the authoritative Phase-1 security baseline and controls.
All Phase-1 implementations must comply with this baseline.
