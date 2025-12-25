# Technology Architecture & Reference Stack
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines the **Technology Architecture** for EAVIP.
It answers the question:

> “Which technologies do we use, where do we use them, and why?”

The intent is to:
- Provide a **reference stack**, not a rigid mandate
- Preserve **vendor neutrality**
- Support **SaaS, BYOC, and On-Prem** deployments
- Enable consistent implementation decisions over time

> Technology choices must serve architecture intent,  
> not constrain it.

---

## Guiding Technology Principles

1. Vendor-neutral by default
2. Cloud-native by design, on-prem compatible
3. Open standards over proprietary protocols
4. Replaceable components via abstraction
5. Operational simplicity over novelty

These principles guide all technology selections.

---

## Technology Domains Overview

EAVIP technology is grouped into the following domains:

1. Application Runtime
2. Data Storage & Persistence
3. Messaging & Eventing
4. Caching
5. Search & Analytics
6. Security & Identity
7. Integration & Connectivity
8. Observability & Operations
9. Frontend & Visualization
10. DevOps & Deployment

Each domain is intentionally decoupled.

---

## 1. Application Runtime

### Chosen Stack
- **Language:** C#
- **Runtime:** .NET (LTS)
- **Architecture Style:** Modular Monolith (initial), Service-ready

### Options Considered
- Java / Spring Boot
- Node.js
- Go

### Why .NET Was Chosen
- Strong DDD and CQRS support
- Excellent performance and tooling
- Long-term LTS guarantees
- Strong enterprise and on-prem adoption
- First-class async and concurrency support

### Trade-offs
- Smaller OSS ecosystem than Node.js
- Higher learning curve than scripting languages

### Decision
.NET is the **primary runtime** for all core services.

---

## 2. Data Storage & Persistence

### Write Model
- **Relational DB:** PostgreSQL (default)
- Alternatives: SQL Server, Oracle (supported)

### Read Model
- **Optimized read schemas**
- Optional denormalization
- Separate read database if needed

### Graph Storage
- **Neo4j** (preferred)
- Alternative: OpenSearch (graph-like queries)

### Why This Split
- Relational DB ensures transactional integrity
- Graph DB enables dependency traversal, impact analysis
- CQRS aligns with architecture analytics use cases

### Trade-offs
- Multiple storage systems increase complexity
- Requires clear ownership and boundaries

---

## 3. Messaging & Eventing

### Supported Modes
- Outbox + Polling (default, safest)
- Kafka
- RabbitMQ
- ActiveMQ
- IBM MQ

### Why Multiple Options
- Enterprises already have messaging investments
- No single broker fits all environments

### Decision
Eventing is **abstracted behind adapters**.
Platform Configuration determines which mode is active.

### Trade-offs
- Adapter maintenance
- Increased testing surface

---

## 4. Caching

### Supported Options
- In-memory cache
- Redis
- Hazelcast

### Use Cases
- Read model acceleration
- Graph query caching
- UI performance optimization

### Why Optional
Caching is an optimization, not a dependency.

---

## 5. Search & Analytics

### Primary Choice
- **OpenSearch**

### Use Cases
- Full-text search across architecture data
- Reporting and analytics
- Time-based queries

### Trade-offs
- Operational overhead
- Requires indexing strategy

---

## 6. Security & Identity

### Supported Mechanisms
- OAuth 2.0 / OIDC
- LDAP / Active Directory
- mTLS
- Certificates
- Managed identities (cloud)

### Secret Management
- HashiCorp Vault
- AWS Secrets Manager
- Azure Key Vault
- GCP Secret Manager

### Core Rule
Secrets are never stored or managed directly by EAVIP.

---

## 7. Integration & Connectivity

### Supported Patterns
- REST APIs
- Webhooks
- Event subscriptions
- Queue-based integration

### Why This Matters
EAVIP must integrate with:
- CI/CD pipelines
- Monitoring tools
- CMDBs
- Cloud providers
- On-prem systems

Integration is a **first-class capability**, not an afterthought.

---

## 8. Observability & Operations

### Supported Tools
- OpenTelemetry
- Prometheus-compatible metrics
- Structured logging
- Distributed tracing

### Why Observability Is Mandatory
EAVIP is an **architecture intelligence system**.
It must observe itself as rigorously as it observes others.

---

## 9. Frontend & Visualization

### Chosen Stack
- React
- TypeScript
- Web-based visualization libraries

### Why This Stack
- Rich UI ecosystem
- Strong visualization support
- Enterprise adoption
- Clear separation from backend logic

### Trade-offs
- Requires frontend skillset
- State management complexity

---

## 10. DevOps & Deployment

### Supported Deployment Models
- SaaS (managed)
- BYOC (customer cloud)
- On-Prem (installer-based)

### Tooling
- Docker
- Kubernetes (optional)
- CI/CD pipelines
- Infrastructure as Code (Terraform-compatible)

### Why This Flexibility
Customer environments vary widely.
Technology architecture must adapt without redesign.

---

## Reference Stack Summary

| Layer | Default Choice | Alternatives |
|-----|---------------|-------------|
| Runtime | .NET | Java |
| Write DB | PostgreSQL | SQL Server, Oracle |
| Graph DB | Neo4j | OpenSearch |
| Messaging | Outbox | Kafka, RabbitMQ |
| Cache | Redis | Hazelcast |
| Search | OpenSearch | Elastic |
| UI | React | — |

---

## Risks & Mitigations

### Risk: Technology Sprawl
**Mitigation:** Clear defaults + adapter pattern

### Risk: Operational Complexity
**Mitigation:** Phase-based adoption

### Risk: Vendor Lock-in
**Mitigation:** Strict abstraction layers

---

## Closing Notes

This technology architecture is **deliberately pragmatic**.
It balances:
- Enterprise reality
- Long-term maintainability
- Architectural purity

The reference stack may evolve, but **principles and boundaries must not**.
