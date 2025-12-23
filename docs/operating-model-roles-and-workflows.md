# Operating Model, Roles & Enterprise Workflows

## Purpose

This document defines **how the Enterprise Architecture Visibility &
Intelligence Platform (EAVIP)** is used in practice across large enterprises.

It answers:
- Who uses the platform?
- For what decisions?
- In what workflows?
- With what accountability?
- At what cadence?

The goal is **adoption, trust, and stickiness** — not shelfware.

---

## Core Philosophy

1. **Architecture is a team sport**
2. **One platform, many personas**
3. **Read-heavy, write-careful**
4. **Governance without friction**
5. **Executives see outcomes, not diagrams**

---

## 1. Core Roles (Enterprise Reality)

### 1.1 Enterprise Architect (EA)

**Primary responsibility**
- Enterprise-wide coherence
- Cross-org alignment
- Target architecture definition

**Uses EAVIP to**
- Navigate enterprise → org → app
- Identify cross-org dependencies
- Detect architecture drift
- Define target-state roadmaps

**Primary views**
- Enterprise dependency map
- Governance dashboards
- Drift & risk heatmaps

---

### 1.2 Solution / Application Architect

**Primary responsibility**
- Application and domain architecture
- HLD / LLD ownership
- Design integrity

**Uses EAVIP to**
- Model application architecture
- Define components and interfaces
- Record ADRs
- Validate dependencies

**Primary views**
- Application drill-down diagrams
- Dependency graphs
- ADR & NFR mappings

---

### 1.3 Engineering Teams

**Primary responsibility**
- Build and evolve systems

**Uses EAVIP to**
- Understand upstream/downstream impact
- Discover existing services
- Validate architecture expectations
- Avoid undocumented dependencies

**Primary views**
- Component-level graphs
- Runtime vs intended views
- Impact analysis

---

### 1.4 Security Architects / Teams

**Primary responsibility**
- Security posture
- Zero-trust enforcement
- Risk reduction

**Uses EAVIP to**
- Visualize trust boundaries
- Inspect auth flows
- Detect security drift
- Review external dependencies

**Primary views**
- Security overlay diagrams
- Trust boundary maps
- Violation dashboards

---

### 1.5 Compliance & Risk Officers

**Primary responsibility**
- Regulatory adherence
- Audit readiness

**Uses EAVIP to**
- Trace controls to architecture
- Review evidence
- Monitor risk exposure

**Primary views**
- Compliance dashboards
- Evidence-linked diagrams
- Risk timelines

---

### 1.6 Platform / Cloud Teams

**Primary responsibility**
- Shared platforms
- Cloud cost & governance

**Uses EAVIP to**
- See who depends on what
- Govern cloud usage
- Manage shared services

**Primary views**
- Cloud deployment views
- Platform dependency maps
- Technology lifecycle views

---

### 1.7 Product Owners / Business Stakeholders

**Primary responsibility**
- Business outcomes
- Delivery alignment

**Uses EAVIP to**
- Understand application landscape
- See risks to delivery
- Align roadmaps with architecture

**Primary views**
- Portfolio views
- Roadmap alignment dashboards

---

### 1.8 Executives (CIO / CTO / CISO)

**Primary responsibility**
- Strategic decisions
- Risk ownership

**Uses EAVIP to**
- See enterprise posture
- Understand transformation impact
- Make evidence-backed decisions

**Primary views**
- Executive summaries
- Trend indicators
- Risk & dependency overviews

---

## 2. Core Operating Workflows

### 2.1 Architecture Discovery & Onboarding

**Trigger**
- New application
- M&A
- New domain

**Flow**
1. Register org / app
2. Import or discover dependencies
3. Validate ownership & data flows
4. Generate baseline diagrams

**Outcome**
- App becomes visible in enterprise graph

---

### 2.2 Design & Change Workflow

**Trigger**
- New feature
- Architectural change

**Flow**
1. Update intended architecture
2. Record ADRs
3. Simulate impact
4. Validate governance rules

**Outcome**
- Approved change with traceability

---

### 2.3 Continuous Validation & Drift Detection

**Trigger**
- CI/CD changes
- Runtime discovery
- Cloud drift

**Flow**
1. Observed data ingested
2. Drift detected
3. Violations classified
4. Teams notified

**Outcome**
- Early correction, not post-mortem

---

### 2.4 Governance & Exception Handling

**Trigger**
- Policy violation
- Risk acceptance request

**Flow**
1. Violation surfaced
2. Impact explained
3. Decision recorded
4. Time-bound acceptance or fix

**Outcome**
- Explicit, auditable governance

---

### 2.5 Transformation & Roadmap Planning

**Trigger**
- Modernization initiative
- Cloud migration
- Decomposition

**Flow**
1. Capture as-is architecture
2. Define to-be state
3. Simulate transitions
4. Track progress vs plan

**Outcome**
- Predictable, controlled transformation

---

### 2.6 Audit & Compliance Review

**Trigger**
- Internal / external audit

**Flow**
1. Select audit time slice
2. Navigate applicable architecture
3. Review controls & evidence
4. Export audit-ready views

**Outcome**
- Reduced audit time, higher confidence

---

## 3. Cadence & Ownership Model

### Cadences
- Daily: Engineers (impact checks)
- Weekly: Architects (drift review)
- Monthly: Governance review
- Quarterly: Portfolio & roadmap review
- Annual: Audit & strategy review

---

### Ownership Rules
- Every node has an owner
- Every decision has an approver
- Every exception has an expiry

No anonymous architecture.

---

## 4. Collaboration Model

- Comments on nodes & edges
- ADR discussions in context
- Shared views for reviews
- Read-only links for stakeholders

Architecture becomes **collaborative, not isolated**.

---

## 5. Why This Operating Model Works

- Aligns with real enterprise roles
- Reduces tool sprawl
- Removes tribal knowledge
- Makes architecture actionable
- Supports both agility and control

---

## What This Model Avoids

- Architecture as a one-time exercise
- PowerPoint-driven reviews
- Security & compliance silos
- Executive blindness
- Tool abandonment

---

## Outcome

With this operating model:
- Architecture becomes **continuous**
- Teams share **one language**
- Decisions are **traceable**
- The enterprise gains **situational awareness**

---

## Status

This document defines the **authoritative operating model** for EAVIP.

All user experiences, permissions, and workflows **must align to this model**.
