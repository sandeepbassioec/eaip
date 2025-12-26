# Technology Selection & Trade-Off Analysis (EAVIP)

## Purpose

This document captures the **explicit technology selection decisions** for
the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It exists to:
- Prevent implicit or emotional technology choices
- Make architectural decisions **defensible and explainable**
- Align with TOGAF Phase D (Technology Architecture)
- Serve as a long-term reference for future architects and teams

No technology choice in EAVIP is accidental.

---

## Architectural Principles Driving Technology Selection

All technology decisions are governed by the following locked principles:

1. Architecture-first, not framework-first
2. Domain integrity over developer convenience
3. Long-term maintainability over short-term velocity
4. Cloud-neutral, vendor-agnostic design
5. Strong ecosystem maturity and hiring feasibility
6. Explicit trade-offs over hidden compromises
7. Learning value for enterprise-scale systems

---

## Backend Technology Selection

### Options Considered

- .NET (C# / ASP.NET Core)
- Java (Spring Boot)
- Node.js (TypeScript / NestJS)
- Go (Golang)

---

### Evaluation Criteria

| Criterion | Importance |
|---------|-----------|
| DDD expressiveness | High |
| Strong typing & domain modeling | High |
| Enterprise tooling maturity | High |
| Performance & scalability | Medium |
| Developer productivity | Medium |
| Hiring & ecosystem | Medium |
| Cloud & on-prem support | High |

---

### Option Analysis

#### Java (Spring Boot)

**Pros**
- Mature enterprise ecosystem
- Strong DDD adoption
- Large talent pool

**Cons**
- Verbosity and boilerplate
- Slower iteration for learning-heavy architecture work
- JVM tuning complexity
- Heavier memory footprint

**Verdict**
❌ Rejected – Too heavyweight for rapid architectural experimentation.

---

#### Node.js (TypeScript)

**Pros**
- Fast development
- Same language frontend & backend
- Good ecosystem

**Cons**
- Weak aggregate enforcement
- Runtime type safety limitations
- Domain invariants harder to protect
- Eventual complexity leakage into handlers

**Verdict**
❌ Rejected – Domain purity and invariants become fragile at scale.

---

#### Go (Golang)

**Pros**
- Excellent performance
- Simple concurrency model
- Easy deployment

**Cons**
- Weak DDD modeling
- Limited expressiveness for rich domains
- Less enterprise tooling
- Learning curve for domain-heavy systems

**Verdict**
❌ Rejected – Optimized for infra, not domain-centric systems.

---

#### .NET (C# / ASP.NET Core) — **SELECTED**

**Pros**
- Excellent DDD expressiveness
- Strong typing & rich domain modeling
- Clean separation of layers
- Mature tooling (EF, MediatR, testing)
- Excellent async & event handling
- Strong cloud + on-prem support

**Cons**
- Requires architectural discipline
- Slightly steeper learning curve than Node.js

**Verdict**
✅ **Selected** – Best balance for enterprise DDD + TOGAF execution.

---

## Frontend Technology Selection

### Options Considered

- React + TypeScript
- Angular
- .NET MAUI / Blazor

---

### Evaluation Criteria

| Criterion | Importance |
|---------|-----------|
| Diagram-heavy UI flexibility | High |
| Ecosystem for visualization | High |
| Long-term maintainability | Medium |
| Hiring availability | Medium |
| Backend decoupling | High |

---

### Option Analysis

#### Angular

**Pros**
- Structured framework
- Enterprise-friendly

**Cons**
- Heavier mental model
- Slower iteration
- Less flexible for dynamic diagram tooling

**Verdict**
❌ Rejected – Too rigid for visualization-heavy architecture tooling.

---

#### .NET MAUI / Blazor

**Pros**
- Shared C# stack
- Strong typing

**Cons**
- Smaller ecosystem
- Limited diagram & graph libraries
- Less mature for complex web visualization

**Verdict**
❌ Rejected – Ecosystem maturity insufficient.

---

#### React + TypeScript — **SELECTED**

**Pros**
- Best-in-class visualization libraries
- Flexible component model
- Large ecosystem (graphs, diagrams, charts)
- Strong hiring availability
- Backend-agnostic

**Cons**
- Requires discipline for large apps

**Verdict**
✅ **Selected** – Best fit for diagram-driven architecture UI.

---

## Messaging & Eventing Technology

### Design Principle

> EAVIP **never hard-codes** messaging technology.

---

### Supported Options

- Kafka
- RabbitMQ
- ActiveMQ
- IBM MQ
- Cloud-native equivalents
- Outbox + polling (fallback)

**Why**
- Customers vary (cloud / on-prem)
- Vendor neutrality is mandatory
- Infrastructure abstraction enforced

**Decision**
✅ Adapter-based messaging layer with pluggable providers.

---

## Data Storage Technology

### Primary Storage

- PostgreSQL (reference implementation)

**Why**
- Strong relational integrity
- Excellent tooling
- Works on cloud & on-prem
- Easy debugging for learning

---

### Graph Storage (Later Phase)

- Neo4j / Graph DB

**Why Deferred**
- Adds complexity
- Not required for Walking Skeleton
- Introduced after correctness is proven

---

## Caching & Search

- Distributed cache: Redis (optional)
- Search & analytics: OpenSearch (later phase)

**Principle**
- Optional capabilities
- Never mandatory for core domain flow

---

## Final Technology Stack (Locked)

| Layer | Technology |
|-----|-----------|
| Frontend | React + TypeScript |
| Backend | .NET 8 / C# |
| Architecture Pattern | DDD + CQRS |
| API | REST (versioned) |
| Messaging | Adapter-based (Kafka/RabbitMQ/etc.) |
| Storage | PostgreSQL |
| Graph (Later) | Neo4j |
| Cache | Redis (optional) |
| Deployment | SaaS / BYOC / On-Prem |

---

## Trade-Off Summary

We intentionally chose:
- **Domain safety over raw speed**
- **Explicit architecture over convenience**
- **Learning depth over shortcuts**
- **Vendor neutrality over lock-in**

These trade-offs align with EAVIP’s mission:
to teach, enforce, and demonstrate **real enterprise architecture**.

---

## Status

This document is:
- Architecture-approved
- Decision-locked
- Required before code execution

No further technology debate is allowed unless constraints change.
