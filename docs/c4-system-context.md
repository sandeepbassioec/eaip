# C4 – System Context Diagram

## Purpose

This document defines the **System Context (C4 Level 1)** for the  
**Enterprise Architecture Intelligence Platform (EAIP)**.

It answers:
- What is EAIP?
- Who uses it?
- What systems does it integrate with?
- Where are the trust and responsibility boundaries?

This is the **highest-level architectural view** and is intended for:
- CTO / CIO
- Enterprise Architects
- Security & Compliance teams
- External stakeholders

---

## System Under Consideration

### Enterprise Architecture Intelligence Platform (EAIP)

EAIP is a **cloud-agnostic, SaaS-based platform** that enables enterprises to:
- Manage application portfolios
- Capture architectural decisions (ADRs)
- Design and govern architectures
- Track transformation roadmaps
- Communicate changes via events and integrations

EAIP acts as the **system of record for enterprise architecture**.

---

## Primary Actors (People)

### Enterprise Architect
- Designs target architectures
- Approves ADRs
- Governs standards

### Solution Architect
- Creates diagrams
- Proposes decisions
- Manages integrations

### Platform / Engineering Teams
- Consume architecture data
- Subscribe to change events
- Integrate pipelines

### Executives (CTO / CIO / Leadership)
- View portfolio health
- Track modernization progress
- Assess risk

---

## External Systems

### Identity Provider (IdP)
Examples:
- Enterprise SSO
- Corporate directory

**Interaction**
- Authenticates users
- Issues identity tokens

---

### Client Applications & Tools

Examples:
- CI/CD pipelines
- Monitoring systems
- Internal tools
- Architecture validation tools

**Interaction**
- Subscribe to EAIP events
- Publish events back to EAIP
- Consume APIs

---

### Client Cloud Environments

Examples:
- AWS
- Azure
- GCP
- Oracle Cloud
- On-Premise

**Interaction**
- Host BYOC deployments
- Receive webhook or queue-based events
- Provide infrastructure context

---

## System Context Diagram (Textual Representation)

+------------------------------------------------------+
| |
| Enterprise Architecture Intelligence Platform |
| (EAIP) |
| |
| - Application Portfolio |
| - ADR Governance |
| - Architecture Modeling |
| - Roadmaps & Transformation |
| - Event Exchange (Webhooks / Queues) |
| |
+-------------------+----------------------------------+
|
|
+-----------+-----------+
| |
| |
+---------------+ +-------------------+
| Human Users | | Client Systems |
| | | |
| Architects | | CI/CD, Tools, |
| Engineers | | Pipelines |
| Leadership | | |
+-------+-------+ +---------+---------+
| |
| |
v v
+----------------+ +-------------------+
| Identity | | Client Cloud |
| Provider (IdP) | | Environments |
| | | (AWS/Azure/etc.) |
+----------------+ +-------------------+


---

## Trust Boundaries

### External Trust Boundary
- Users and systems authenticate via Identity Provider
- All access is authenticated and authorized

### Platform Trust Boundary
- Workspace-level isolation
- Role and permission enforcement
- Audit and compliance controls

### Integration Trust Boundary
- Signed webhook payloads
- Workspace-scoped API keys
- Explicit subscription management

---

## Key Architectural Characteristics

- EAIP is the **central authority**
- External systems are **loosely coupled**
- All interactions are:
  - Versioned
  - Auditable
  - Event-driven where possible

---

## Out of Scope for System Context

- Internal microservices
- Database technologies
- Cloud-specific deployments
- Implementation details

These will be covered in **C4 Container & Component diagrams**.

---

## Status

This document defines the **authoritative System Context** for EAIP.

All lower-level architecture diagrams must align with this view.

