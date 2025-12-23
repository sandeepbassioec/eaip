# Reference Implementation – Frontend (Execution Guide)

## Purpose

This document defines the **authoritative frontend reference implementation**
for **EAVIP**, aligned with the UI interaction model, API contracts,
and MVP scope.

It answers:
- How the frontend is structured
- How drill-down navigation is implemented
- How diagrams stay synchronized with the Enterprise Graph
- How state, permissions, and time context are handled

This is an **execution guide**, not a UI mockup.

---

## Frontend Core Principles (Locked)

1. **The Enterprise Graph drives UI state**
2. **Drill-down is semantic, not visual**
3. **All views are derived, never edited**
4. **Time context is global**
5. **Performance over ornamentation**
6. **No UI-only truth**

---

## Recommended Technology Stack (Reference)

> Replaceable, but proven.

- Framework: React
- Language: TypeScript
- State Management: Zustand / Redux Toolkit
- Data Fetching: React Query
- Visualization: D3 / Cytoscape / Mermaid (generated)
- Routing: React Router
- Styling: CSS Modules / Tailwind
- Auth: OAuth2 / OIDC (token-based)

---

## High-Level Application Structure
src/
├── app/
│ ├── AppShell.tsx
│ ├── Router.tsx
│ └── Layout.tsx
│
├── modules/
│ ├── enterprise/
│ ├── organization/
│ ├── application/
│ ├── component/
│ ├── dependency/
│ └── documents/
│
├── graph/
│ ├── queries/
│ ├── selectors/
│ └── overlays/
│
├── state/
│ ├── authStore.ts
│ ├── timeContextStore.ts
│ └── uiStateStore.ts
│
├── api/
│ ├── client.ts
│ └── contracts.ts
│
└── shared/
├── components/
├── hooks/
└── utils/


Each module corresponds to a **drill-down level**.

---

## Routing & Drill-Down Model

### Canonical Routes
/enterprise
/org/:orgId
/app/:appId
/component/:componentId
/dependency/:dependencyId


Rules:
- Route change = semantic context change
- Routes are deep-linkable
- Back/forward always works

---

## Global State Model

### Global Stores

- `authStore`
  - user
  - roles
  - permissions

- `timeContextStore`
  - now | historical | planned
  - timestamp

- `uiStateStore`
  - filters
  - overlays
  - selected entity

No business data is stored globally.

---

## Data Fetching Strategy

- React Query for all API calls
- Queries keyed by:
  - entityId
  - timeContext
  - filters

### Example
```ts
useQuery(
  ['applicationGraph', appId, timeContext],
  fetchApplicationGraph
)
```
All data is:
* Read-only
* Cached
* Invalidated on context change
---

Diagram Rendering Model
Rules
* Diagrams are rendered from API responses
* No manual editing
* No client-side graph mutations

Flow
API Graph Data
 → Normalize
 → Layout Engine
 → Diagram Renderer

| Role      | Behavior                   |
| --------- | -------------------------- |
| Viewer    | Read-only, limited depth   |
| Architect | Full drill-down, proposals |
| Executive | Summary-first views        |
