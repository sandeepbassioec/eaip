# EAVIP – State Continuation & Context Lock

## Purpose

This document is the **authoritative context anchor** for the
**Enterprise Architecture Visibility & Intelligence Platform (EAVIP)**.

It exists to:
- Preserve architectural intent across sessions
- Eliminate repeated explanations
- Enable seamless continuation after tab closure, browser crash, reboot, or long gaps
- Act as the single “resume point” for future design discussions

This file overrides conversational memory.

---

## Product Name

**Enterprise Architecture Visibility & Intelligence Platform (EAVIP)**

---

## Product Intent (Non-Negotiable)

Build a **CAST Highlight–class (and beyond)** enterprise platform that provides:

- Full enterprise architecture visibility under one roof
- Drill-down navigation:
  - Enterprise → Organization → Application → Component
- Accurate representation of:
  - Data flows
  - Dependencies (inter-app, inter-org, inter-component)
  - Governance, security, and compliance
- Auto-generated diagrams from a single canonical model
- Continuous drift detection between intent and reality

---

## Core Architectural Principles (Locked)

1. The **Enterprise Graph** is the single source of truth
2. Diagrams, reports, and dashboards are **derived**, never authoritative
3. Architecture intent and observed reality are modeled separately
4. History is immutable and time-aware
5. Governance is continuous and explainable
6. Cloud-native by design, cloud-neutral by architecture
7. On-Prem is supported via disciplined capability abstraction
8. Integrations are adapter-based, not vendor-bound
9. Humans approve decisions; systems surface impact
10. No silent drift is allowed

---

## Canonical Building Blocks (Locked)

### Enterprise Graph
- Property graph model
- Nodes, relationships, temporal validity
- Manual + observed + derived inputs
- Append-only history

### Auto-Generated Diagrams
- C4 (Context, Container, Component, Deployment)
- Data Flow Diagrams
- Trust Boundary & Security Diagrams
- Cloud & Infrastructure Diagrams

### Governance & Drift Detection
- Declarative policies
- Intent vs observed comparison
- Explainable violations

### Security & Zero Trust
- Trust boundaries as first-class entities
- Identity, auth flows, data sensitivity
- Security overlays on architecture

### Compliance & Risk
- Regulations, standards, controls as graph entities
- Evidence & audit replay
- Time-aware compliance posture

### Deployment Models
- SaaS (AWS-first reference)
- BYOC (any cloud)
- On-Prem (customer-managed, curated capabilities)

### Eventing & Integration
- Webhooks supported everywhere (cloud + on-prem)
- Queues supported everywhere via adapters:
  - Kafka
  - RabbitMQ
  - ActiveMQ / IBM MQ
  - Cloud equivalents
- Platform uses abstractions, not vendor services

### Observability & Architecture Intelligence
- Runtime telemetry enriches the graph
- Drift detection from runtime signals
- Hot paths and criticality scoring

### APIs & SDKs
- REST for commands and proposals
- Read-only graph query APIs
- Event-driven integrations
- SDKs for JS, .NET, Java, Python
- Strong versioning and backward compatibility

### Transformation & Roadmaps
- As-Is vs To-Be modeling
- What-if simulations
- Dependency-driven sequencing
- Measurable progress tracking

---

## Documentation Strategy (Locked)

- Markdown (`.md`) is the primary format
- Documents are first-class citizens
- Documents attach to graph entities
- Full-text + contextual indexing
- GitHub-friendly structure
- A master `index.md` will be generated **at the very end**

---

## Locked Decisions

- Decision: AWS will be the default reference cloud provider  
  Status: Locked

- Decision: Platform will be cloud-neutral and support SaaS, BYOC, and On-Prem deployments  
  Status: Locked

- Decision: On-Prem deployments will support webhooks and queues via customer-managed infrastructure  
  Details:
  - Webhooks over HTTP/mTLS
  - Queues via Kafka, RabbitMQ, ActiveMQ, IBM MQ
  Status: Locked

- Decision: The Enterprise Graph is the single source of truth; all views are derived  
  Status: Locked

- Decision: Eventing and integrations will use abstractions, not cloud-vendor services  
  Status: Locked

- Decision: A strict State Update Protocol will be followed  
  Details:
  - The assistant must explicitly specify which sections to ADD, UPDATE, or NOT TOUCH
  - The user will only perform instructed changes
  Status: Locked

---

## Completed Major Topics

- Enterprise Graph Model
- Data Ingestion & Auto-Diagram Generation
- Governance, Validation & Drift Detection
- Security Architecture & Zero Trust Mapping
- Compliance, Risk & Regulatory Mapping
- Operating Model & Roles
- Permissions, Access Control & Authorization
- Extensibility, Plugins & Ecosystem Model
- Observability, Telemetry & Architecture Intelligence
- Deployment Architecture & Packaging Strategy
- Data Storage, Persistence & Graph Scaling Strategy
- API Design, SDKs & Integration Contracts
- Transformation, Modernization & Roadmap Intelligence
- Enterprise Graph Schema & Query Model
- 
---

## Current Progress Pointer

LAST COMPLETED:
Enterprise Graph Schema & Query Model

NEXT TOPIC:
API Specification (Concrete Endpoints & Contracts)

---

## State Update Protocol (Non-Negotiable)

This protocol exists to ensure **session-to-session continuity** without
ambiguity, memory loss, or repeated explanations.

### Rules

1. At the end of **every session**, the assistant must provide:
   - Exact section names to update
   - Clear instruction whether to ADD, UPDATE, or NOT TOUCH
   - Copy–paste ready content

2. The user must:
   - Update only the sections explicitly mentioned
   - Never infer or guess changes
   - Never modify sections marked as "DO NOT TOUCH"

3. `state-continuation.md` is a **living state document**, not a chat log:
   - Current truth sections are UPDATED
   - Decision and history sections are APPENDED
   - Full rewrites are forbidden

4. If update instructions are not explicitly provided,
   **no changes should be made** to the state file.

5. This protocol overrides conversational assumptions and memory.

### Enforcement

- The assistant is responsible for correctness of instructions
- The user is responsible only for copy–paste execution
- No re-interpretation or debate is allowed once locked

This protocol is **locked** and must be followed for the lifetime of the project.

---

## Session Change Log

### Checkpoint – Pre-Reporting Phase
- All core architecture, governance, deployment, storage, API, and transformation pillars completed
- State Update Protocol locked and formalized
- System ready to proceed to executive reporting and value realization

### Session – Execution-Level Technical Deep Dive Started
- Added concrete Enterprise Graph schema and query model
- Transitioned from conceptual design to execution-grade specifications
- Prepared groundwork for concrete API specifications
