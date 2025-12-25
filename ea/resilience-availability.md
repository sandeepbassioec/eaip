# Resilience, Availability & Failure Management
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how EAVIP remains available, resilient, and predictable**
in the face of failures.

It answers:
- What happens when things fail
- How failures are isolated
- How the platform recovers
- How architecture intelligence remains trustworthy during incidents

This aligns with:
- TOGAF Phase D (Technology Architecture)
- Enterprise resilience principles
- SRE-inspired failure thinking

> Systems don’t fail because failures occur.  
> Systems fail because **failures were not anticipated**.

---

## Core Resilience Principles (Locked)

1. Failure is expected, not exceptional
2. Failures must be isolated
3. Recovery must be automated
4. Partial availability is acceptable
5. Architecture truth must never be corrupted
6. Resilience over raw performance

These principles guide all decisions.

---

## Availability Targets (Guidance)

EAVIP targets **tiered availability**, not uniform SLAs.

| Capability | Availability Target |
|-----------|---------------------|
| Architecture Core | Very High |
| Governance | High |
| Visualization | Medium |
| Reporting | Medium |
| Metrics & Intelligence | Medium |
| Integrations | Variable |

> Not all failures deserve the same urgency.

---

## Failure Domains

EAVIP explicitly recognizes these failure domains:

1. Service-level failure
2. Data store failure
3. Integration failure
4. Network failure
5. Infrastructure failure
6. Human error

Each domain is addressed separately.

---

## Service-Level Resilience

### Patterns Used
- Bulkheads
- Circuit breakers
- Timeouts
- Retries with backoff

### Why
Prevents cascading failures and protects critical services.

---

## Data Layer Resilience

### Relational Database
- Replication
- Backups
- Point-in-time recovery

### Graph Database
- Read replicas
- Periodic snapshots

### Rule (Locked)
> Write integrity is more important than availability.

If needed, EAVIP prefers **read-only mode** over inconsistent writes.

---

## Eventing & Integration Resilience

### Outbox Pattern (Mandatory)
Ensures:
- No lost events
- No duplicate side effects
- Safe retries

### Broker Failures
- Events queued locally
- Delivery resumes automatically
- No synchronous dependency on brokers

---

## Partial Degradation Strategy

EAVIP is designed to **degrade gracefully**.

### Examples
- Visualization unavailable → Core remains usable
- Metrics unavailable → Architecture still editable
- Integration down → Events queued

This preserves trust during incidents.

---

## Isolation Strategy

### Service Isolation
- Each service runs independently
- No shared memory
- No shared databases

### Tenant Isolation (SaaS)
- Logical isolation
- Strict access boundaries
- Separate failure blast radius

---

## Disaster Recovery (DR)

### RPO / RTO Guidance

| Component | RPO | RTO |
|--------|-----|-----|
| Architecture Core | Low | Medium |
| Governance | Medium | Medium |
| Reporting | Higher | Higher |

Actual values depend on deployment model.

---

## Human Error Mitigation

### Controls
- Approval workflows
- Immutable history
- Audit trails
- Rollback support

### Why
Most outages are human-induced, not technical.

---

## Observability for Resilience

### Signals Monitored
- Service health
- Event backlog
- Write failures
- Dependency health

These signals feed **architecture intelligence**, not just ops dashboards.

---

## Trade-offs

**Pros**
- Predictable behavior during failures
- Reduced blast radius
- Enterprise-grade reliability

**Cons**
- Higher design complexity
- More components to operate

---

## Why This Architecture Is Best

- Accepts reality of distributed systems
- Prioritizes architectural integrity
- Supports regulated environments
- Scales across deployment models

---

## Closing Notes

Resilience is not about preventing failure.
It is about **containing failure**.

EAVIP’s design ensures that:
- Failures are visible
- Impact is limited
- Recovery is deliberate

---

## Next Logical Step (Major Transition)

👉 **Opportunities, Solutions & Execution Planning (TOGAF Phase E)**  
(file: `ea/opportunities-solutions.md`)

Say **`next`** when ready.
