# Multi-Tenancy Isolation (Deep Dive)

## Purpose

This document defines the **multi-tenancy isolation model** for the
**Enterprise Architecture Intelligence Platform (EAIP)**.

It specifies:
- Tenant isolation levels
- Data, compute, and network boundaries
- Security guarantees
- SaaS and BYOC coexistence
- Operational and compliance implications

This document is **authoritative** for all tenancy decisions.

---

## Core Principles

1. Tenant isolation is **by design**, not by convention
2. Isolation level is **configurable per workspace**
3. Same codebase supports **all isolation modes**
4. No cross-tenant data access — ever
5. Compliance requirements drive isolation choice

---

## Isolation Levels Overview

EAIP supports **three isolation levels**.

| Level | Name | Use Case |
|------:|------|----------|
| L1 | Logical Isolation | Default SaaS |
| L2 | Physical Isolation | Regulated SaaS |
| L3 | BYOC Isolation | Enterprise / Regulated |

---

## Level 1: Logical Isolation (Default SaaS)

### Description
All tenants share the same infrastructure, with **strict logical boundaries**.

### Characteristics
- TenantId present on every record
- Query-level enforcement
- Per-tenant encryption keys (logical)
- Shared compute and storage

### Guarantees
- No cross-tenant reads or writes
- Independent throttling and quotas
- Independent access control

### Pros
- Lowest cost
- Fast onboarding
- Simplest operations

### Cons
- Not suitable for extreme regulatory requirements

---

## Level 2: Physical Isolation (Dedicated Resources)

### Description
Tenants get **dedicated data stores** while sharing control plane services.

### Characteristics
- Separate databases per tenant
- Separate object storage buckets
- Shared application services
- Dedicated encryption keys

### Guarantees
- Strong data isolation
- Reduced blast radius
- Compliance-friendly

### Pros
- Meets many regulatory needs
- Still centrally managed

### Cons
- Higher cost
- More operational overhead

---

## Level 3: BYOC Isolation (Bring Your Own Cloud)

### Description
EAIP is deployed into the **customer’s cloud account**.

### Characteristics
- Customer owns infrastructure
- Platform provides deployment artifacts
- Control plane optionally external
- Data plane fully customer-controlled

### Guarantees
- Full data sovereignty
- Network-level isolation
- Customer-managed compliance

### Pros
- Maximum trust
- Meets strict regulatory demands

### Cons
- Slower onboarding
- Customer operational responsibility

---

## Control Plane vs Data Plane

### Control Plane
- Identity & access
- Architecture modeling
- ADR governance
- Event routing logic

### Data Plane
- Webhook delivery
- Queue integrations
- Client-specific extensions

**Rule:**  
Control plane **never directly accesses** tenant data plane resources.

---

## Tenant Context Propagation

### Mandatory Context
- TenantId
- WorkspaceId
- IsolationLevel
- ComplianceFlags

### Enforcement Points
- API Gateway
- Application services
- Event routing
- Data access layer

Violation = **hard failure + audit event**

---

## Event Isolation

### Internal Events
- Always tagged with TenantId
- Routed only to same-tenant consumers

### External Events
- Workspace-scoped subscriptions
- Dedicated secrets per tenant
- Independent retry & DLQ

---

## Security Boundaries

### Identity
- Workspace-scoped identities
- No global admin access to tenant data

### Data
- Encryption at rest & transit
- Per-tenant key isolation

### Network (L3)
- VPC / VNet isolation
- Customer-controlled ingress/egress

---

## Compliance Mapping

| Requirement | L1 | L2 | L3 |
|------------|----|----|----|
| SOC 2 | ✅ | ✅ | ✅ |
| ISO 27001 | ✅ | ✅ | ✅ |
| Data Residency | ⚠️ | ✅ | ✅ |
| Regulated Industries | ❌ | ⚠️ | ✅ |

---

## Operational Considerations

### Scaling
- L1: Horizontal, shared
- L2: Per-tenant scaling
- L3: Customer-managed

### Monitoring
- Metrics always tenant-scoped
- Alerts isolated per tenant

### Incident Response
- Tenant-specific blast radius
- Isolation level determines response scope

---

## Forbidden Anti-Patterns

❌ Global admin access to tenant data  
❌ Shared encryption keys  
❌ Cross-tenant event consumption  
❌ Tenant context inferred implicitly  
❌ Mixing tenants in read models  

---

## Outcome

With this model:
- EAIP supports **true enterprise SaaS**
- BYOC is first-class, not an afterthought
- Compliance is architectural, not procedural
- Tenants trust the platform at scale

---

## Status

This document defines the **official multi-tenancy isolation strategy**.

Any change to tenant handling, data access, or deployment models **must update this file**.
