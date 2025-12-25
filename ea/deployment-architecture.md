# Deployment Architecture & Infrastructure Topology
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how EAVIP is deployed across environments** and how
infrastructure topology supports:

- SaaS
- BYOC (Bring Your Own Cloud)
- On-Prem installations

It answers:
> “Where do services run, how do they communicate, and how do we remain
cloud-neutral without sacrificing enterprise-grade reliability?”

This aligns with **TOGAF Phase D (Technology Architecture)** and prepares
for **Phase E (Opportunities & Solutions)**.

---

## Deployment Design Goals

1. Cloud-neutral by design
2. First-class on-prem support
3. Zero-trust networking
4. Horizontal scalability
5. Failure isolation
6. Minimal operational burden for customers

---

## Deployment Models Supported (Locked)

### 1. SaaS (EAVIP-Managed)

- Hosted and operated by EAVIP
- Multi-tenant logical isolation
- Shared infrastructure, isolated data

**Use Case**
Customers who want fastest onboarding with minimal ops overhead.

---

### 2. BYOC (Customer Cloud)

- Deployed into customer’s cloud account
- Uses customer-managed infrastructure
- Logical isolation per tenant

**Use Case**
Customers with strict data residency or compliance requirements.

---

### 3. On-Prem (Customer-Managed)

- Installed via installer or deployment bundle
- Runs in customer data center
- Integrates with existing infra

**Use Case**
Highly regulated or legacy-heavy enterprises.

---

## Core Infrastructure Topology

### Logical Zones

1. Edge / Access Zone
2. Application Zone
3. Data Zone
4. Integration Zone
5. Management Zone

This zoning applies across all deployment models.

---

## 1. Edge / Access Zone

### Components
- Load balancer
- API Gateway
- WAF (optional)

### Responsibilities
- TLS termination
- Authentication enforcement
- Rate limiting

### Why This Zone Exists
Security must be enforced **before** traffic enters core services.

---

## 2. Application Zone

### Components
- Architecture Core Service
- Governance Service
- Metrics & Intelligence Service
- Visualization Service
- Integration Service
- Reporting Service

### Deployment Strategy
- Containerized services
- Scalable horizontally
- Stateless where possible

### Why Stateless First
- Simplifies scaling
- Enables resilience
- Supports multiple environments

---

## 3. Data Zone

### Components
- Relational Database (PostgreSQL / SQL Server)
- Graph Database (Neo4j)
- Search Engine (OpenSearch)
- Cache (Redis)

### Rules (Locked)
- No direct access from Edge
- Access only via Application Zone
- Network isolation mandatory

---

## 4. Integration Zone

### Components
- Message brokers (Kafka / RabbitMQ / MQ)
- Webhook dispatchers
- Outbox processors

### Why Separate Zone
- Integrations are failure-prone
- Must not cascade failures into core services

---

## 5. Management Zone

### Components
- Observability stack
- Logging & tracing
- Admin tools
- Backup & recovery

### Why Separate
Operations must be isolated from business workloads.

---

## Deployment Patterns

### Containerization

- Docker images
- Immutable deployments
- Versioned artifacts

### Orchestration Options

- Kubernetes (preferred)
- Docker Compose (on-prem / dev)
- VM-based fallback (on-prem legacy)

---

## Networking Model (Zero Trust)

### Principles
- No implicit trust between services
- mTLS for service-to-service
- Explicit allow lists

### Why Zero Trust
Architecture platforms are **high-value targets**.

---

## Secrets & Configuration Management

### Rules (Locked)

- No secrets in code
- No secrets in config files
- No secrets in logs

### Supported Mechanisms
- Vault
- Cloud secret managers
- Customer-managed stores (on-prem)

EAVIP stores **references only**.

---

## High Availability & Resilience

### Strategies
- Horizontal scaling
- Circuit breakers
- Retry with backoff
- Bulkheads per service

### Why This Matters
Architecture platforms must be available during incidents,
not just during normal operations.

---

## Failure Scenarios & Isolation

| Failure | Impact | Mitigation |
|------|-------|------------|
| Metrics service down | No insights | Core remains operational |
| Integration broker down | Delayed events | Outbox retries |
| Visualization failure | UI degraded | Core unaffected |
| DB outage | Write blocked | Read-only fallback |

---

## Trade-offs

**Pros**
- Strong isolation
- Cloud/on-prem parity
- Secure by default

**Cons**
- Higher initial setup complexity
- Requires ops maturity

---

## Why This Architecture Is Best

- Supports enterprise diversity
- Avoids vendor lock-in
- Enables gradual adoption
- Aligns with TOGAF & DDD

---

## Closing Notes

Deployment architecture is where **design meets reality**.

This model ensures:
- Architecture intent survives deployment
- Customers retain control
- EAVIP scales with enterprise needs

---

## Next Logical Step

👉 **Data Storage Strategy & Persistence Patterns**  
(file: `ea/data-persistence.md`)

Say **`next`** and we continue.
