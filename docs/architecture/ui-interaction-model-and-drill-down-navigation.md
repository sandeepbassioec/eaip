# UI Interaction Model & Drill-Down Navigation

## Purpose

This document defines the **authoritative UI interaction model** for EAVIP.

It specifies:
- How users navigate the enterprise
- How drill-down works across levels
- How diagrams, data, and documents stay synchronized
- How complexity is revealed progressively without overwhelming users

This is the **contract between architecture, UX, and frontend engineering**.

---

## Core UI Principles (Locked)

1. **Progressive disclosure over information overload**
2. **One canonical graph, many synchronized views**
3. **Every visual element is clickable**
4. **Drill-down is semantic, not visual-only**
5. **No dead ends in navigation**
6. **Zoom ≠ Drill-down (they are different actions)**

---

## 1. Primary Navigation Model

### 1.1 Hierarchical Levels (Authoritative)

The platform enforces a **semantic hierarchy**:
Enterprise
└── Organization
└── Application
└── Component
└── Dependency / Data Flow


Users can **enter at any level** (based on role),
but drill-down always follows this semantic order.

---

## 2. Entry Points into the UI

Users can start from:

- Enterprise overview dashboard
- Organization-specific view
- Application catalog
- Search results
- Shared deep links
- Executive reports

Regardless of entry point, **navigation rules remain consistent**.

---

## 3. Enterprise-Level View

### What Users See
- Organizations as primary nodes
- High-level inter-org data flows
- Risk, compliance, and dependency heatmaps
- Aggregate metrics only (no component noise)

### Allowed Actions
- Click organization → drill down
- Filter by domain, risk, criticality
- Switch time context (past / present / planned)

### Disallowed
- Component-level detail
- Raw dependency graphs

---

## 4. Organization-Level View

### What Users See
- Applications within the organization
- Cross-org integrations
- Ownership and accountability overlays
- Compliance and policy posture

### Allowed Actions
- Click application → drill down
- Highlight inbound/outbound dependencies
- View org-scoped documents and ADRs

---

## 5. Application-Level View

### What Users See
- C4 Container-style diagram
- Components/services
- Interfaces (APIs, events)
- Data stores
- External system interactions

### Allowed Actions
- Click component → drill down
- Toggle data flows on/off
- Overlay runtime signals
- Open application-specific documents

### Key Rule
> **Application view is the most frequently used view — it must be fast and clean.**

---

## 6. Component-Level View

### What Users See
- Detailed component graph
- Dependencies (calls, events, data access)
- Trust boundaries
- Security and data sensitivity overlays

### Allowed Actions
- Click dependency → inspect
- Perform impact analysis
- View historical changes
- Compare As-Is vs To-Be

---

## 7. Dependency & Data Flow Inspection

### Dependency Panel Includes
- Source and target
- Relationship type (CALLS, EMITS, READS_FROM, etc.)
- Protocol and data sensitivity
- Governing policies
- Violations (if any)
- Approval history

Dependencies are **first-class citizens**, not lines on a diagram.

---

## 8. Drill-Down vs Zoom (Important Distinction)

### Zoom
- Visual scaling only
- No semantic change
- Used for readability

### Drill-Down
- Semantic navigation
- Context changes
- New data fetched
- URL changes (deep-linkable)

---

## 9. View Synchronization Model

All UI panels are synchronized:

| Action | Result |
|-----|-------|
| Click node in diagram | Details panel updates |
| Change time context | Diagram + data refresh |
| Apply filter | All views re-render |
| Select dependency | Diagram highlights path |

No view operates in isolation.

---

## 10. Time Context in UI

Time context selector is **global**:
- Now (current state)
- Historical (past snapshot)
- Planned (To-Be)

Changing time context:
- Re-renders diagrams
- Updates metrics
- Switches document versions

---

## 11. Search & Jump Navigation

Search supports:
- Organizations
- Applications
- Components
- Dependencies
- Documents

Search results always link to the **correct drill-down level**.

---

## 12. Role-Based UI Behavior

### Viewers
- Read-only
- Limited drill-down depth

### Architects
- Full navigation
- Impact analysis
- Proposal initiation

### Executives
- Summary-first
- Drill-down optional
- No component clutter by default

---

## 13. Diagram Interaction Rules

- Diagrams are **generated, not drawn**
- Manual edits are forbidden
- Users interact via:
  - Selection
  - Filtering
  - Overlay toggles
  - Drill-down

This preserves consistency with the Enterprise Graph.

---

## 14. URL & Deep Linking Model

Every meaningful view is deep-linkable:
/enterprise
/org/{id}
/app/{id}
/component/{id}
/dependency/{id}


URLs encode:
- Entity
- Time context
- Filters (where applicable)

---

## 15. What This UI Model Avoids

- Static diagrams
- Conflicting views
- UI-only state
- Screenshot-driven understanding
- Manual synchronization

---

## Outcome

With this interaction model:
- Users never feel lost
- Complexity is revealed gradually
- Diagrams stay truthful
- Navigation mirrors enterprise reality
- EAVIP feels intuitive despite depth

---

## Status

This document defines the **authoritative UI interaction and drill-down model**.

All frontend design and implementation **must conform** to this specification.


