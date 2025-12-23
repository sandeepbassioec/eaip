# MVP Backlog & Sprint-Level Breakdown

## Purpose

This document defines the **execution-ready MVP backlog** for EAVIP.

It translates architecture into:
- Concrete user stories
- Sprint-level sequencing
- Clear inclusion/exclusion boundaries
- A delivery plan that proves value fast without breaking the long-term design

This is the **handoff document from architecture to engineering execution**.

---

## MVP Definition (Locked)

### MVP Goal

> Enable architects to **visually explore enterprise architecture**,  
> model applications and dependencies,  
> and auto-generate truthful diagrams from a single source of truth.

### MVP Success Test

- Architects voluntarily use EAVIP instead of static diagrams
- One org can model and explore its architecture end-to-end
- Drill-down works reliably across levels
- No governance bypasses are required

---

## MVP Scope (In / Out)

### ✅ IN SCOPE (Strict)

- Enterprise → Org → App → Component hierarchy
- Manual creation of core entities
- Dependency modeling (CALLS, EMITS, READS, WRITES)
- Read-only graph queries
- Auto-generated diagrams (basic C4)
- Drill-down navigation
- Markdown document attachment
- Basic RBAC (Viewer / Architect)
- Time context: **Now only**

---

### ❌ OUT OF SCOPE (Intentionally)

- Runtime observability
- Drift detection
- Advanced governance rules
- Executive dashboards
- Plugins / marketplace
- AI-assisted insights
- As-Is vs To-Be comparison
- Historical time travel

---

## MVP Architecture Constraints

- Single-tenant implementation acceptable (tenant-aware design required)
- Manual data entry first
- No automation dependencies
- No background discovery agents
- Feature flags for future expansion

---

## Sprint Plan Overview

| Sprint | Focus |
|------|------|
| Sprint 0 | Foundations & setup |
| Sprint 1 | Enterprise graph core |
| Sprint 2 | Application & dependency modeling |
| Sprint 3 | Graph queries & diagrams |
| Sprint 4 | UI drill-down & navigation |
| Sprint 5 | Hardening & MVP readiness |

Each sprint is **2 weeks**.

---

## Sprint 0 – Foundations

### Goals
- Enable productive development
- Lock engineering discipline

### Stories
- Repo setup with agreed structure
- Base service scaffolding
- Auth stub & identity context
- State-continuation discipline
- CI pipeline skeleton

### Deliverable
> A stable foundation ready for real features.

---

## Sprint 1 – Enterprise Graph Core

### Goals
- Implement canonical graph model

### Stories
- Node schema implementation
- Relationship schema implementation
- Temporal fields support
- Event emission on change
- Persistence abstraction

### Deliverable
> Graph can store and retrieve enterprise structure.

---

## Sprint 2 – Application & Dependency Modeling

### Goals
- Model real architecture elements

### Stories
- Create organization API
- Create application API
- Create component API
- Propose dependency API
- Dependency validation rules

### Deliverable
> Core architecture can be modeled end-to-end.

---

## Sprint 3 – Graph Queries & Auto-Diagrams

### Goals
- Enable exploration and visualization

### Stories
- Impact analysis query
- Bounded traversal logic
- Diagram generation service
- C4-style container diagrams
- Read-only graph APIs

### Deliverable
> Architecture is visible and explorable.

---

## Sprint 4 – UI Drill-Down & Navigation

### Goals
- Make the system usable

### Stories
- Enterprise overview UI
- Organization drill-down
- Application diagram view
- Component detail view
- Dependency inspection panel
- Global time context (Now)

### Deliverable
> Users can navigate without confusion.

---

## Sprint 5 – Hardening & MVP Readiness

### Goals
- Prepare for real users

### Stories
- RBAC enforcement
- Error handling & validation
- Performance guardrails
- Basic audit logging
- Documentation cleanup
- MVP demo scenarios

### Deliverable
> MVP is stable, demoable, and adoption-ready.

---

## Definition of Done (MVP)

- All APIs documented
- All core flows demoable
- No critical security gaps
- No manual diagram editing
- Clear upgrade path to Phase 2

---

## MVP Risks & Mitigations

| Risk | Mitigation |
|----|-----------|
| Overbuilding | Strict scope enforcement |
| UX complexity | Progressive disclosure |
| Performance issues | Query guards |
| Design drift | State-continuation discipline |

---

## What This MVP Avoids

- Feature creep
- Premature intelligence
- Executive-only views
- Automation before correctness
- One-off hacks

---

## Outcome

With this MVP:
- Architecture visibility is proven
- Adoption feedback is real
- Core design is validated
- Phase-2 investment is justified

---

## Status

This document defines the **authoritative MVP backlog and sprint plan**.

All Phase-1 execution **must conform** to this plan.
