# UI Wireframes & Screen Flow Specification

## Purpose

This document defines the **low-fidelity UI wireframes and screen flows**
for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It focuses on:
- Screen responsibilities (not visuals)
- User flow correctness
- Drill-down consistency
- Role-based experience differences

This is a **UX execution contract**, not a design mockup.

## Core UX Principles (Locked)

1. Function before aesthetics
2. One screen = one primary intent
3. Drill-down always changes semantic context
4. No screen exists without a graph backing it
5. Executives see summaries first, architects see structure first
6. No dead-end screens

## Primary Screens (Authoritative)

### 1. Enterprise Overview Screen

Purpose:
- Provide enterprise-level visibility
- Show organizations and cross-org relationships

Contains:
- Organization tiles / nodes
- High-level dependency heatmap
- Risk and compliance indicators
- Global time context selector

Primary Actions:
- Click organization → Organization Screen
- Apply filters (risk, domain, criticality)

Disallowed:
- Component visibility
- Raw dependency lists

---

### 2. Organization Screen

Purpose:
- Show architecture within a single organization

Contains:
- Application catalog
- Cross-organization integrations
- Ownership and accountability info
- Organization-scoped documents

Primary Actions:
- Click application → Application Screen
- Highlight inbound / outbound dependencies

---

### 3. Application Screen (Core Screen)

Purpose:
- Show application-level architecture truth

Contains:
- Container-level diagram
- Components and interfaces
- External system connections
- Data stores
- Attached documents (ADRs)

Primary Actions:
- Click component → Component Screen
- Toggle data flows
- Open impact analysis

This is the **most frequently used screen**.

---

### 4. Component Screen

Purpose:
- Show detailed runtime and dependency context

Contains:
- Component dependency graph
- Trust boundaries
- Security and data sensitivity overlays
- Historical changes

Primary Actions:
- Inspect dependencies
- Run impact analysis
- Compare As-Is vs To-Be (later phases)

---

### 5. Dependency Inspection Screen / Panel

Purpose:
- Explain a single dependency clearly

Contains:
- Source and target
- Relationship type
- Protocol
- Data classification
- Governing policies
- Approval and audit history

Primary Actions:
- Navigate to source component
- Navigate to target component

Dependencies are **first-class**, not visual lines.

---

### 6. Document Viewer Screen

Purpose:
- Provide contextual architecture documentation

Contains:
- Markdown viewer
- Version history
- Linked entities
- Approval status

Primary Actions:
- Navigate to linked architecture entity
- View historical versions

Editing is governed and role-restricted.

---

### 7. Executive Dashboard Screen

Purpose:
- Provide decision-ready summaries

Contains:
- Architecture health indicators
- Risk trends
- Transformation progress
- Value realization metrics

Primary Actions:
- Drill down to supporting evidence
- Switch time context

Executives are never forced into component views.

---

## Navigation Flow Rules

- Enterprise → Organization → Application → Component → Dependency
- Search can jump to any level
- Back navigation always restores previous context
- URLs always represent current state

## Role-Based Screen Access

Viewer:
- Read-only
- Limited drill-down depth

Architect:
- Full navigation
- Proposal initiation
- Impact analysis

Executive:
- Summary screens first
- Drill-down optional
- Simplified defaults

## Screen State Rules

- All screens are derived from API data
- No local mutations
- Time context change refreshes entire screen
- Filters are explicit and visible

## What This UX Model Avoids

- Static diagrams
- Hidden navigation paths
- UI-only state
- Ambiguous drill-down behavior
- Screen overload

## Outcome

With this wireframe and flow model:
- Users always know where they are
- Navigation mirrors enterprise structure
- Complexity is revealed progressively
- UX remains scalable as scope grows

## Status

This document defines the **authoritative UI wireframe and screen flow specification**.
All UX and frontend implementation must conform to this model.
