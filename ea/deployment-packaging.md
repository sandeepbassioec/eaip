# Deployment Models, Packaging & Distribution Strategy
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how EAVIP is deployed, packaged, and distributed**
across different customer environments while preserving:

- Architectural integrity
- Vendor neutrality
- Governance guarantees
- Operational simplicity

It explains:
- SaaS vs BYOC vs On-Prem deployment models
- What changes and what stays constant across models
- Packaging units and boundaries
- Upgrade, migration, and rollback strategies
- Why these choices are made and what trade-offs they introduce

This document is a **reference deployment architecture**.

---

## Core Principle (Locked)

**Deployment model must never change the logical architecture,
domain behavior, or governance guarantees of the platform.**

Only infrastructure and operational responsibilities may vary.

---

## Supported Deployment Models

EAVIP officially supports **three deployment models**:

1. SaaS (Vendor-Managed)
2. BYOC – Bring Your Own Cloud
3. On-Prem (Customer-Managed)

All three models share the same logical architecture.

---

## 1. SaaS Deployment Model (Reference)

### Description

- Fully managed by EAVIP vendor
- Hosted in AWS (default reference)
- Multi-tenant, logically isolated

### Characteristics

- Fastest onboarding
- Zero infrastructure responsibility for customers
- Standardized upgrades and patches
- Usage-based pricing

### Responsibilities

| Area | Owner |
|---|---|
| Infrastructure | EAVIP |
| Security baseline | EAVIP |
| Upgrades | EAVIP |
| Data isolation | EAVIP |
| Compliance posture | Shared |

---

## 2. BYOC – Bring Your Own Cloud

### Description

- Deployed into customer-owned cloud account
- AWS / Azure / GCP supported
- Vendor provides automation & templates

### Characteristics

- Strong data sovereignty
- Customer controls networking and identity
- Vendor manages application lifecycle (optionally)

### Responsibilities

| Area | Owner |
|---|---|
| Infrastructure | Customer |
| Application runtime | EAVIP |
| Identity integration | Customer |
| Compliance controls | Shared |

### Why BYOC Exists

- Regulatory constraints
- Security-sensitive enterprises
- Reduced vendor lock-in perception

---

## 3. On-Prem Deployment Model

### Description

- Fully customer-managed infrastructure
- Deployed in data center or private cloud
- Air-gapped supported (with constraints)

### Characteristics

- Maximum control
- Highest operational responsibility
- Slower upgrades
- Requires mature IT operations

### Responsibilities

| Area | Owner |
|---|---|
| Infrastructure | Customer |
| Security | Customer |
| Upgrades | Customer (guided) |
| Monitoring | Customer |

---

## Common Logical Architecture (Invariant)

Across all models, the following remain **identical**:

- Domain model
- Enterprise Graph schema
- Governance workflows
- Decision lifecycle
- Security model (Zero Trust)
- API contracts
- Event semantics

Deployment never alters business meaning.

---

## Packaging Units

EAVIP is packaged into **clear, bounded units**:

### Core Platform Services
- Architecture Repository
- Metrics & Decision Engine
- Governance Engine
- Visualization Engine
- Reporting Engine

### Supporting Services
- Integration & Event Exchange
- Search / Indexing
- Identity adapters
- Secret resolution adapters

---

## Packaging Format

### Cloud (SaaS / BYOC)
- Containerized services
- Helm / IaC-based provisioning
- Environment-specific configuration

### On-Prem
- Container images + manifests
- Optional VM-based bundles
- Offline installation packages

No code changes across environments.

---

## Configuration vs Code (Critical Rule)

**All environment differences are expressed via configuration,
never via conditional code paths.**

Configuration sources:
- Platform Configuration Aggregate
- Environment descriptors
- Adapter selection

This preserves testability and correctness.

---

## Upgrade Strategy

### SaaS
- Rolling upgrades
- Backward-compatible API evolution
- Zero downtime where possible

### BYOC
- Vendor-guided upgrades
- Version pinning supported
- Customer-approved rollout

### On-Prem
- Explicit upgrade packages
- Pre-flight validation
- Rollback-supported releases

---

## Migration & Backward Compatibility

Rules:
- Data migrations are versioned
- Schema evolution is additive
- No destructive migrations without governance approval
- Historical data is preserved

Architecture history is never rewritten.

---

## Failure & Rollback Strategy

Each deployment supports:
- Health checks
- Canary releases (where possible)
- Rollback to last known good state
- State consistency validation

Governance ensures rollback decisions are recorded.

---

## Security Across Deployment Models

Invariant security guarantees:
- Zero Trust enforcement
- Identity-first access
- Audit logging
- Policy evaluation

Only identity providers and secret sources vary.

---

## Trade-offs

**SaaS**
- + Speed, simplicity
- – Less infrastructure control

**BYOC**
- + Sovereignty, flexibility
- – More coordination required

**On-Prem**
- + Full control
- – Operational burden

EAVIP deliberately supports all three to maximize adoption.

---

## Why This Strategy Works

- Preserves architectural intent
- Avoids forked implementations
- Supports enterprise diversity
- Enables phased adoption

Deployment becomes a choice, not a constraint.

---

## Final Mental Model

- One architecture
- Multiple execution environments
- Zero compromise on governance
- Configuration over customization

---

## Next Step

Proceed to **Commercial Model, Licensing & Tenant Isolation Strategy**  
File: `ea/commercial-licensing.md`
