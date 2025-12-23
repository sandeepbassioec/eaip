# Drill-Down Visualization & Interaction Model

## Purpose

This document defines **how users interact with the Enterprise Graph**:
- Drill-down (zoom in)
- Roll-up (zoom out)
- Lateral exploration (trace flows)
- Time travel (past / present / target)
- Governance context (why this exists)

It specifies **interaction semantics**, not UI technology.

---

## Design Principles

1. **Graph-first interactions**
2. **No dead ends** — every view is navigable
3. **Context preserved at all times**
4. **Time is always visible**
5. **Intent and reality are comparable**
6. **One interaction = one clear question answered**

---

## 1. Zoom & Drill-Down Semantics

### 1.1 Zoom Levels (Canonical)

| Level | Focus | What You See |
|------:|------|--------------|
| L0 | Enterprise | Organizations, shared platforms, cross-org flows |
| L1 | Organization | Applications, domains, inter-org dependencies |
| L2 | Application | Components, interfaces, data stores |
| L3 | Component | APIs, events, schemas, controls |
| L4 | Detail | ADRs, requirements, NFRs, security, compliance |

> **Rule:** Zooming never changes truth — it changes **projection density**.

---

### 1.2 Double-Click Behavior (Zoom In)

- Double-click **node**
  - Traverses its primary ownership relationship
  - Applies node-specific layout
  - Preserves filters and time

Examples:
- Double-click *Enterprise* → Organizations
- Double-click *Organization* → Applications
- Double-click *Application* → Components

---

### 1.3 Zoom Out / Roll-Up

- Single breadcrumb click
- Mouse back gesture
- Keyboard shortcut

**Guarantee:** Users can always return to origin without losing state.

---

## 2. Lateral Exploration (Trace & Follow)

### 2.1 Dependency Tracing

Actions:
- “Show inbound dependencies”
- “Show outbound dependencies”
- “Show cross-org flows only”

Visual treatment:
- Highlighted paths
- Dim non-relevant nodes
- Directional arrows emphasized

---

### 2.2 Data Flow Tracing

- Producer → Consumer highlighting
- Data sensitivity overlay
- Boundary crossings emphasized

Use cases:
- Impact analysis
- Compliance exposure
- Incident investigation

---

## 3. Context Preservation Model

### 3.1 Context Stack

Every interaction pushes context:

[Enterprise] → [Org A] → [App X] → [Component Y]

Context carries:
- Origin node
- Traversal path
- Applied filters
- Time slice

---

### 3.2 Breadcrumbs (Always Visible)

Breadcrumbs show:
- Where you are
- How you got here
- Quick jump points

Breadcrumbs are **semantic**, not just navigation.

---

## 4. Time Slider & Temporal Views

### 4.1 Time Slider (Global Control)

The time slider controls:
- Node visibility
- Relationship validity
- Versioned architectures

Modes:
- As-Is (observed)
- To-Be (planned)
- Historical (past snapshot)

---

### 4.2 Time-Aware Visual Cues

- Expired relationships: faded / dashed
- Planned relationships: dotted
- Current relationships: solid

This allows:
- Architecture evolution playback
- Drift detection
- Change simulation

---

## 5. Intent vs Reality Comparison

### 5.1 Dual Overlay Mode

Users can toggle:
- **Intended architecture**
- **Observed architecture**
- **Diff view**

Diff view highlights:
- Missing components
- Unexpected dependencies
- Policy violations

---

### 5.2 Why This Exists (Explainability)

Every node / edge can answer:
- “Why is this here?”
- “Who approved this?”
- “What requirement does this satisfy?”

Backed by:
- ADR links
- Requirement links
- Audit trail

---

## 6. Context Menus (Right-Click Semantics)

Context menus are **node-type aware**.

### Examples:
- Application node:
  - View architecture
  - Trace impact
  - Open ADRs
  - View security posture
- Data flow edge:
  - View contract
  - View data sensitivity
  - View compliance controls

---

## 7. Filtering & Focus

### 7.1 Filters (Non-Destructive)

Filters never delete data — they **mask**.

Common filters:
- Organization
- Domain
- Technology
- Risk level
- Compliance scope

---

### 7.2 Focus Mode

Focus mode:
- Isolates selected path
- Hides unrelated nodes
- Preserves orientation

Used for:
- Presentations
- Reviews
- Incident analysis

---

## 8. Cross-View Synchronization

All views are synchronized:
- Graph
- Diagram
- Tables
- Dashboards

Selecting a node in one:
- Highlights it everywhere
- Preserves time and filters

---

## 9. Visual Encoding Standards

### 9.1 Shape Semantics
- Rounded rectangles: Applications
- Rectangles: Components
- Cylinders: Data stores
- Diamonds: Decisions / Controls

### 9.2 Color Semantics
- Color = responsibility / boundary
- Red = risk / violation
- Yellow = warning / planned
- Green = compliant / healthy

> **Rule:** Color never encodes two meanings.

---

## 10. Performance & Scale Considerations

- Progressive rendering
- Lazy expansion on zoom
- Edge bundling for dense graphs
- Maximum visible nodes per view

Users should **never feel overwhelmed**.

---

## 11. What This Model Avoids

- Static diagrams
- Page reload navigation
- Hard-coded hierarchies
- Loss of context on zoom
- Tool-specific gestures

---

## Outcome

With this interaction model:
- Enterprise architecture becomes **explorable**
- Impact becomes **intuitive**
- Governance becomes **explainable**
- Change becomes **predictable**

---

## Status

This document defines the **authoritative interaction semantics** for EAVIP.

All UI, APIs, and visualization components **must conform** to these rules.
