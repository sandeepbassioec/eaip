# Deployment Architecture & Packaging Strategy
(SaaS, BYOC, and On-Prem)

## Purpose

This document defines **how EAVIP is packaged, deployed, upgraded, and operated**
across **SaaS**, **BYOC**, and **On-Prem** environments.

The goals are:
- Predictable deployments
- Safe upgrades
- Clear responsibility boundaries
- No architectural forks
- Support for air-gapped environments

---

## Core Principles

1. **One codebase, multiple deployment profiles**
2. **Packaging adapts; architecture does not**
3. **Stateless services, stateful graph**
4. **Upgrades are reversible**
5. **Customer controls runtime in BYOC / On-Prem**
6. **No hidden cloud dependencies**

---

## 1. Deployment Profiles (Authoritative)

| Profile | Owner | Typical Customer |
|------|------|------------------|
| SaaS | Platform | Cloud-native enterprises |
| BYOC | Customer | Regulated / large enterprises |
| On-Prem | Customer | Air-gapped / legacy / gov |

Each profile differs only in:
- Infrastructure provisioning
- Runtime ownership
- Operations responsibility

---

## 2. Logical Deployment Architecture (Common)

All deployments contain the same **logical services**:

- API Gateway
- Graph Service
- Ingestion Services
- Diagram & View Services
- Governance Engine
- Event Exchange
- Plugin Runtime
- Document Service
- Identity Integration
- Persistence Layer

> **Rule:**  
> No service is “SaaS-only” by design.

---

## 3. Packaging Units

### 3.1 Container Images (Primary)

All services are packaged as:
- OCI-compliant containers
- Versioned and signed
- Minimal base images

Used by:
- SaaS
- BYOC
- On-Prem (if Kubernetes available)

---

### 3.2 Helm Charts (Preferred)

Helm is the **reference deployment format**.

Supports:
- SaaS internal
- BYOC clusters
- Customer-managed Kubernetes
- OpenShift

Charts expose:
- Capability flags
- Integration adapters
- Resource limits
- Secrets references

---

### 3.3 Non-Kubernetes Packaging (On-Prem)

For environments without Kubernetes:
- Docker Compose
- Systemd-based services
- VM-based deployment bundles

Feature set remains the same; scaling is manual.

---

## 4. Infrastructure Responsibilities

### SaaS
- Platform provisions infra
- Managed databases
- Managed queues
- Managed identity

### BYOC
- Customer provisions infra
- Platform provides:
  - Helm charts
  - Reference Terraform (optional)
- Customer controls:
  - Network
  - Identity
  - Secrets

### On-Prem
- Customer provisions everything
- Platform provides:
  - Installers
  - Validation scripts
  - Health checks

---

## 5. Eventing & Integration Packaging

### 5.1 Webhooks
- Always enabled
- Configurable endpoints
- mTLS / signed headers

### 5.2 Queue Adapters (Pluggable)
- Kafka
- RabbitMQ
- ActiveMQ / IBM MQ
- Cloud equivalents

Adapters are:
- Optional
- Independently deployable
- Capability-flagged

---

## 6. Identity & Access Integration

| Environment | Identity Strategy |
|-----------|------------------|
| SaaS | Platform IdP |
| BYOC | Customer IAM |
| On-Prem | LDAP / AD / Local |

Identity is **externalized** in all cases.

---

## 7. Configuration & Secrets Management

- No secrets in images
- Environment-specific config
- Supports:
  - Vaults
  - KMS
  - On-Prem HSM
  - Encrypted files (air-gapped)

---

## 8. Upgrade & Versioning Strategy (CRITICAL)

### 8.1 Versioning
- Semantic versioning
- Backward-compatible graph migrations
- API versioning

---

### 8.2 Upgrade Flow
1. Validate environment
2. Apply schema migrations
3. Roll services gradually
4. Validate health
5. Finalize

---

### 8.3 Rollback
- Stateless services → instant rollback
- Graph → forward-only with versioned history
- Feature flags for safe disable

---

## 9. Air-Gapped & Restricted Environments

On-Prem supports:
- Offline installers
- Local image registries
- Manual update bundles
- No outbound calls required

Telemetry & plugins are **opt-in**.

---

## 10. Observability of the Platform Itself

Every deployment exposes:
- Health endpoints
- Metrics
- Audit logs

But:
> Platform observability never leaks tenant data.

---

## 11. Responsibility Matrix (Clear & Honest)

| Area | SaaS | BYOC | On-Prem |
|----|----|----|----|
| Availability | Platform | Shared | Customer |
| Scaling | Platform | Customer | Customer |
| Security Patching | Platform | Shared | Customer |
| Backups | Platform | Customer | Customer |
| Compliance | Shared | Customer | Customer |

---

## 12. What This Strategy Avoids

- Separate products per deployment
- Cloud-specific logic in core
- Feature parity lies
- Fragile installers
- “Works only in SaaS” syndrome

---

## Outcome

With this strategy:
- Enterprises choose **how** to run EAVIP
- Architecture stays **clean**
- Operations are **predictable**
- Trust increases across regulated customers
- Sales friction reduces dramatically

---

## Status

This document defines the **authoritative deployment and packaging strategy**.

All CI/CD, installers, and ops tooling **must conform** to this model.
