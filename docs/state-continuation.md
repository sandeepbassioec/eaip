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

### Architecture Intelligence & Decision Support (Locked)

The platform will provide advanced architecture intelligence capabilities,
beyond static visualization, including:

- Architecture "Why Layer":
  Every major architectural structure must trace back to explicit rationale
  (ADR, business capability, regulatory need, or trade-off).

- Blast Radius Simulation:
  Ability to simulate failures, changes, or deprecations and understand
  cross-org, compliance, risk, and business impact.

- Architecture Confidence Scoring:
  Every entity and relationship will carry a confidence score based on
  validation source, freshness, and ownership.

- Architecture Optionality Index:
  Measurement of how easily systems can change based on coupling,
  dependency depth, and vendor lock-in.

- Decision Regret Tracking:
  Long-term tracking of architectural decisions versus actual outcomes
  to enable organizational learning.

These capabilities are first-class platform features, not optional add-ons.

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

- Decision: Diagram-level inline creation of entities will require mandatory user confirmation
  Details:
  - Inline actions on diagrams must trigger a confirmation popup
  - Two modes are enforced:
    1. Link an existing entity
    2. Create a new entity via proposal workflow
  - No silent graph mutations are allowed
  - Governance workflows apply identically to diagram-initiated changes
  Status: Locked

- Decision: The platform will include Architecture Confidence Scoring
  Details:
  - Confidence reflects trustworthiness of architecture data
  - Based on source, validation, observation, and recency
  Status: Locked

- Decision: The platform will support Blast Radius Simulation
  Details:
  - Failure, change, and deprecation scenarios
  - Impact across organizations, compliance, risk, and value
  Status: Locked

- Decision: Architecture Optionality Index will be computed
  Details:
  - Measures structural agility and change readiness
  - Used in executive reporting and transformation planning
  Status: Locked

- Decision: Architecture "Why Layer" will be mandatory for major structures
  Details:
  - All significant architecture must trace back to explicit rationale
  Status: Locked

- Decision: Decision Regret Tracking will be supported
  Details:
  - Outcomes of ADRs tracked over time
  - Enables learning-oriented architecture governance
  Status: Locked

- Decision: Platform execution will follow a phased roadmap
  Details:
  - Delivery will be organized into explicit phases
  - Each phase has clear objectives and exit criteria
  - No phase auto-rolls into the next without review
  Status: Locked

- Decision: Phase-1 scope and epics are strictly locked
  Details:
  - Phase-1 is limited to core modeling, governance, diagrams, documents, and read-only reporting
  - Advanced intelligence, observability, plugins, and AI are explicitly excluded
  - No Phase-2/3 capability may leak into Phase-1
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
- API Specification (Concrete Endpoints & Contracts)
- UI Interaction Model & Drill-Down Navigation
- MVP Backlog & Sprint Breakdown
- Backend Reference Implementation
- Frontend Reference Implementation
- Infrastructure & Deployment Reference
- Security Review, Threat Modeling & Abuse Cases
- UI Wireframes & Screen Flows
- Governance Workflows & Decision Lifecycle
- Document Management, Indexing & Search
- Diagram Interaction & Inline Creation Rules
- Reporting & Executive Dashboards
- Value Realization & ROI Modeling
- Observability & Architecture Drift Detection
- Plugin & Extension Framework
- Commercial Model & Licensing
- Master Documentation Index (docs/index.md)
- Advanced Architecture Intelligence & Decision Support (Concept Locked)
- Roadmap & Phased Execution Plan
- Phase 1 Prioritization & Epic Breakdown (MVP Execution)

---

## Current Progress Pointer

LAST COMPLETED:
Commercial Model & Licensing + Master Documentation Index

NEXT TOPIC:
Stabilization Phase / Review / Optional Enhancements

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
   
7. Exception Rule:
   - The single-copyable-markdown-block rule does NOT apply to `state-continuation.md`
   - This file may use multiple sections for clarity
   - The assistant must explicitly state ADD / UPDATE / NOT TOUCH instructions
   Status: Locked


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

### Checkpoint – Core Platform Definition Completed
- All foundational platform documents completed
- Governance, security, compliance, reporting, value, observability, extensibility, and commercial models finalized
- Master documentation index generated
- Platform definition reached execution-ready maturity

### Session – Advanced Architecture Intelligence Locked
- Identified and locked next-generation EA differentiators
- Platform scope extended beyond visualization into decision intelligence
- Confidence scoring, blast radius simulation, optionality index, and decision learning locked as future capabilities

### Session – Phased Execution Roadmap Locked
- Execution roadmap defined from Foundation through Market Leadership
- Phases sequenced to preserve architectural integrity
- Decision gates and exit criteria formalized

### Session – Phase-1 MVP Execution Scope Locked
- Phase-1 epics and non-goals finalized
- MVP scope protected against feature leakage
- Execution-ready breakdown prepared for engineering teams
