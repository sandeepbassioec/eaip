# Data Ingestion, Dependency Discovery & Auto-Generated Diagrams

## Purpose

This document defines **how real-world information enters the Enterprise Graph**
and how **all architecture diagrams are automatically generated** from that graph.

It explicitly covers:
- Inter-application dependencies
- Inter-component dependencies
- Cross-organization dependencies
- External systems, libraries, and SaaS
- Cloud infrastructure and managed services

The outcome:
> **One source of truth → infinite accurate views**

---

## Core Principle (Non-Negotiable)

> **Diagrams are never manually authoritative.  
> The Enterprise Graph is.**

All diagrams are:
- Generated from graph data
- Regenerated on change
- Time-aware and versioned

---

## 1. Dependency Types We Must Capture (Exhaustive)

### 1.1 Inter-Application Dependencies

Examples:
- App A calls App B API
- App A publishes events consumed by App B
- App A reads App B database (legacy)
- App A sends files to App B

Captured as relationships:
- CALLS
- PUBLISHES / SUBSCRIBES
- READS / WRITES
- TRANSFERS

---

### 1.2 Inter-Component Dependencies (Inside an Application)

Examples:
- Service → Service calls
- Component → Database
- Component → Message broker
- Component → Cache

Captured as:
- CONTAINS (Application → Component)
- CALLS (Component → Component)
- READS / WRITES (Component → DataStore)

---

### 1.3 Cross-Organization Dependencies (CRITICAL)

Examples:
- Org A → Org B application integration
- Shared platforms (IAM, Payments, Data)
- Regulatory boundary crossings

Captured as:
- SHARES_WITH (Organization ↔ Organization)
- TRANSFERS (Data across org boundary)
- DEPENDS_ON (Platform-level)

These relationships are **first-class risk and compliance signals**.

---

### 1.4 External Dependencies

Includes:
- Third-party SaaS (Stripe, Salesforce, etc.)
- External partner APIs
- Open-source libraries
- Vendor-managed platforms

Modeled as nodes:
- ExternalApplication
- ExternalService
- ExternalLibrary
- Vendor

Captured as:
- DEPENDS_ON
- CALLS
- HOSTED_BY
- LICENSED_FROM

---

### 1.5 Cloud & Infrastructure Dependencies (MANDATORY)

Cloud is **not a footnote** — it is architecture.

Modeled entities:
- CloudProvider
- Account / Subscription
- Region / Zone
- ManagedService
- Compute
- Network
- Storage

Relationships:
- DEPLOYED_ON
- CONNECTS_TO
- SECURED_BY
- LOCATED_IN

Supports:
- AWS
- Azure
- GCP
- Oracle Cloud
- On-Prem

---

## 2. Data Ingestion Channels (HOW reality enters)

### 2.1 Manual Modeling (Architect Input)
- UI-based graph edits
- ADR-backed changes
- Intent definition

Used for:
- Target architecture
- Governance
- Design-time truth

---

### 2.2 Structured Imports
- CSV / Excel
- Open APIs
- CMDB exports
- Cloud inventory dumps

Mapped to:
- Applications
- Components
- Dependencies
- Ownership

---

### 2.3 CI/CD & Build-Time Signals
- Build pipelines
- Dependency manifests
- IaC templates
- Artifact metadata

Used to detect:
- Component relationships
- Library usage
- Platform coupling

---

### 2.4 Cloud Discovery
- Cloud APIs
- Resource graphs
- Network topology

Used to detect:
- Deployment reality
- Environment drift
- Shadow dependencies

---

### 2.5 Runtime & Observability Feeds (Optional but Powerful)
- Traces
- Service maps
- Network flows

Used to detect:
- Actual runtime calls
- Undocumented dependencies
- Performance impact paths

---

## 3. Normalization into the Enterprise Graph

All inputs (manual or automated):
- Normalize into **node + relationship model**
- Annotated with:
  - Source (manual / observed / imported)
  - Confidence
  - Timestamp
  - Environment

This enables:
- Intent vs reality comparison
- Drift detection
- Trust scoring

---

## 4. Automatic Diagram Generation (THE MAGIC)

### 4.1 Diagram = Graph Projection

A diagram is defined by:
- Start node
- Relationship types
- Depth
- Filters
- Layout rules

Nothing else.

---

### 4.2 Auto-Generated Diagram Types

#### Enterprise Context Diagram
- Enterprise → Organizations
- Cross-org flows highlighted

#### Organization Architecture Diagram
- Org → Applications
- External dependencies visible

#### Application Architecture (C4)
- App → Components
- APIs, events, data stores

#### Data Flow Diagram
- Producer → Consumer
- Sensitivity & ownership overlays

#### Deployment Diagram
- Application → Cloud services
- Regions, networks, boundaries

---

### 4.3 Regeneration Rules

- Any graph change → diagram version bump
- Time slider controls historical versions
- Manual layout hints allowed, but data-driven

---

## 5. Layout Intelligence (So Diagrams Look “Mast”)

Layout rules consider:
- Ownership boundaries
- Dependency direction
- Org separation
- Cloud regions

Examples:
- Cross-org flows always drawn across boundaries
- External dependencies always on edges
- Core systems centered, leaf systems peripheral

---

## 6. Explainability (WHY THIS EDGE EXISTS)

Every auto-generated edge can answer:
- Source of truth (manual, CI/CD, runtime)
- ADR that justified it
- Time when it appeared
- Risk / compliance impact

---

## 7. Governance & Validation

Rules:
- Undocumented runtime dependency → violation
- Cross-org data flow without contract → risk
- Deprecated technology in use → warning

These surface **directly on diagrams**.

---

## 8. What This Achieves (WHY THIS IS HUGE)

With this model:
- No stale diagrams
- No tribal knowledge
- No hidden dependencies
- No architecture theater

The enterprise can **see itself thinking and moving**.

---

## What This Deliberately Avoids

- Diagram-first modeling
- Manual sync between tools
- Cloud-specific lock-in
- Code-only dependency graphs

---

## Status

This document defines the **authoritative ingestion and auto-diagram model**.

All future:
- Discovery features
- Integrations
- Visualizations

**must conform to this model**.
