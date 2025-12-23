# Phase 1 Prioritization & Epic Breakdown (MVP Execution)

## Purpose

This document defines the **authoritative Phase-1 (MVP) prioritization and epic breakdown**
for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It converts the roadmap into:
- Executable epics
- Clear scope boundaries
- Explicit non-goals
- Measurable exit criteria

This is the **delivery blueprint** for Phase-1 execution.

---

## Phase-1 Objective (Locked)

Deliver a **usable, trustworthy enterprise architecture platform**
that enables real enterprises to model, govern, and visualize their architecture
without manual diagrams or uncontrolled drift.

Phase-1 proves:
- The Enterprise Graph works
- Diagrams are truthful
- Governance is usable
- The platform can be adopted

---

## Phase-1 Scope Boundaries (Non-Negotiable)

### INCLUDED
- Manual architecture modeling
- Auto-generated diagrams
- Basic governance workflows
- Document attachment
- Read-only executive visibility

### EXCLUDED
- Runtime observability
- Drift detection
- Advanced intelligence
- Plugin framework
- AI assistance

No Phase-2/3 features may leak into Phase-1.

---

## Phase-1 Epics (Authoritative)

### EPIC 1 — Enterprise Graph Core

Purpose:
- Establish the canonical source of truth

Includes:
- Node types: Enterprise, Org, App, Component, Dependency
- Relationship rules and validation
- Temporal validity
- Append-only history
- Confidence metadata (structural only)

Exit Criteria:
- Graph can represent a real enterprise
- History is immutable
- All views derive from the graph

---

### EPIC 2 — Manual Modeling & CRUD Workflows

Purpose:
- Allow architects to define intent explicitly

Includes:
- Create/update flows for all core entities
- Inline creation support (with confirmation)
- Ownership and metadata capture
- Validation before persistence

Exit Criteria:
- No silent mutations
- Governance triggers correctly
- Entities are consistently modeled

---

### EPIC 3 — Auto-Generated Diagrams (Core Views)

Purpose:
- Replace manual diagrams completely

Includes:
- Enterprise overview
- Organization application map
- Application container view
- Component dependency view
- Deterministic layout rules

Exit Criteria:
- Diagrams regenerate from graph only
- No manual positioning
- Role-aware filtering works

---

### EPIC 4 — Governance & Proposal Workflow

Purpose:
- Control architectural change

Includes:
- Proposal creation
- Review and approval flows
- Policy validation (basic)
- Audit trail generation

Exit Criteria:
- No direct graph mutation
- Decisions are traceable
- Governance is usable, not blocking

---

### EPIC 5 — Document Management (MVP)

Purpose:
- Anchor architecture decisions and designs

Includes:
- Markdown document upload
- Entity attachment
- Versioning
- Basic full-text indexing

Exit Criteria:
- Documents are searchable
- Documents are context-bound
- ADRs are first-class

---

### EPIC 6 — Read-Only Executive Reporting

Purpose:
- Provide leadership visibility without complexity

Includes:
- High-level architecture health metrics
- Risk indicators (derived)
- Application inventory summaries

Exit Criteria:
- Executives can consume without training
- Metrics trace back to graph evidence

---

### EPIC 7 — SaaS Reference Deployment

Purpose:
- Prove production viability

Includes:
- AWS-based reference deployment
- Environment separation
- Secure defaults
- Observability (platform health only)

Exit Criteria:
- Platform runs in production-like setup
- Security posture validated
- Deployment is repeatable

---

## Phase-1 Non-Goals (Explicit)

- Runtime telemetry ingestion
- Drift detection
- Plugin execution
- Advanced analytics
- AI-generated insights
- Industry benchmarking

Any request in these areas is deferred.

---

## Phase-1 Success Criteria (Definition of Done)

Phase-1 is complete when:
- A real enterprise can model its architecture end-to-end
- Diagrams replace PowerPoint
- Governance decisions are auditable
- Executives trust what they see
- No architectural shortcuts exist

---

## Risk Controls

- Scope creep prevention via epic boundaries
- No speculative optimizations
- Feature flags over branching
- Early enterprise pilot validation

---

## Outcome

With Phase-1 executed:
- The platform is **credible**
- The architecture foundation is **clean**
- Advanced intelligence can be layered safely
- Customer trust is established early

---

## Status

This document defines the **authoritative Phase-1 prioritization and epic breakdown**.
All Phase-1 execution must conform to this scope.
