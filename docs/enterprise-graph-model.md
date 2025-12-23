# Enterprise Graph Model (Conceptual)

## Purpose

This document defines the **Enterprise Graph Model** that powers the
Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

The graph is the **single source of truth** for:
- Enterprise structure
- Application and data flows
- Dependencies and impact analysis
- Architecture intent vs reality
- Drill-down navigation

All diagrams, analytics, and governance views are **derived from this graph**.

---

## Core Principles

1. **Graph-first, Diagram-second**
2. **Everything is a node or a relationship**
3. **Relationships are directional and typed**
4. **Time is a first-class dimension**
5. **Drill-down is graph traversal**
6. **Reality and intent coexist**

---

## 1. Graph Fundamentals

### 1.1 Graph Type

- **Directed graph**
- **Attributed nodes and edges**
- **Multi-edge allowed** between same nodes
- **Temporal (time-aware)**

(Node) --[RELATIONSHIP]--> (Node)


---

## 2. Node Taxonomy (WHAT exists)

Nodes represent **things** in the enterprise.

---

### 2.1 Enterprise-Level Nodes

| Node Type | Description |
|---------|-------------|
| Enterprise | Top-level boundary |
| Organization | Legal / business entity |
| BusinessUnit | Operational grouping |
| Domain | Business or technical domain |

---

### 2.2 Application-Level Nodes

| Node Type | Description |
|---------|-------------|
| Application | Logical application |
| Component | Internal module / service |
| Interface | API, event, file, UI |
| Job | Batch / scheduled process |

---

### 2.3 Data-Level Nodes

| Node Type | Description |
|---------|-------------|
| DataEntity | Business data concept |
| DataStore | Database / storage |
| Schema | Logical schema |
| Dataset | Shared / published data |

---

### 2.4 Architecture & Governance Nodes

| Node Type | Description |
|---------|-------------|
| Diagram | View generated from graph |
| ADR | Architecture Decision |
| Requirement | Functional / NFR |
| Control | Security / compliance control |

---

### 2.5 Technology Nodes

| Node Type | Description |
|---------|-------------|
| Technology | Language, framework |
| Platform | Cloud / runtime platform |
| Vendor | External provider |

---

### 2.6 Change & Time Nodes

| Node Type | Description |
|---------|-------------|
| Roadmap | Planned evolution |
| Milestone | Change checkpoint |
| Version | Snapshot in time |

---

## 3. Relationship Taxonomy (HOW things connect)

Relationships represent **meaningful connections**.

---

### 3.1 Structural Relationships

| Relationship | From → To |
|-------------|-----------|
| OWNS | Organization → Application |
| CONTAINS | Application → Component |
| BELONGS_TO | Component → Domain |
| HOSTED_ON | Application → Platform |

---

### 3.2 Dependency Relationships (CRITICAL)

| Relationship | Meaning |
|-------------|--------|
| CALLS | Sync API dependency |
| PUBLISHES | Emits event |
| SUBSCRIBES | Consumes event |
| READS | Reads data |
| WRITES | Writes data |
| DEPENDS_ON | Generic dependency |

All dependency relationships are:
- **Directional**
- **Typed**
- **Traversable for impact analysis**

---

### 3.3 Data Flow Relationships

| Relationship | Meaning |
|-------------|--------|
| PRODUCES | Creates data |
| CONSUMES | Uses data |
| TRANSFERS | Moves data across boundary |
| SHARES_WITH | Cross-org data sharing |

Each data flow relationship carries:
- Data sensitivity
- Frequency
- Contract reference

---

### 3.4 Governance Relationships

| Relationship | Meaning |
|-------------|--------|
| DECIDED_BY | Architecture → ADR |
| SATISFIES | Component → Requirement |
| VIOLATES | Component → Control |
| APPROVED_FOR | Technology → Domain |

---

### 3.5 Time & Change Relationships

| Relationship | Meaning |
|-------------|--------|
| SUPERSEDES | Version → Version |
| EVOLVES_TO | Architecture → Target |
| PLANNED_IN | Change → Roadmap |

---

## 4. Time Dimension (WHEN)

### 4.1 Temporal Properties

Every node and relationship can have:

- `validFrom`
- `validTo`
- `observedAt`
- `plannedAt`

This enables:
- As-Is architecture
- To-Be architecture
- Historical replay
- Future simulation

---

### 4.2 Time-Based Queries

Examples:
- “Show dependencies **as of last quarter**”
- “What will this architecture look like **after migration**?”
- “When did this dependency appear?”

---

## 5. Intent vs Reality Modeling

### 5.1 Dual Reality Model

The graph explicitly distinguishes:

| Aspect | Meaning |
|-----|--------|
| INTENDED | Designed / approved |
| OBSERVED | Detected / actual |

Same relationship type can exist twice:
- Intended (from ADR / diagram)
- Observed (from runtime / discovery)

**Drift = difference between the two**

---

## 6. Drill-Down Mechanics (KEY TO YOUR VISION)

### 6.1 Drill-Down = Graph Traversal

Example:
- Double-click Enterprise  
  → Traverse `OWNS` → Organizations
- Double-click Organization  
  → Traverse `OWNS` → Applications
- Double-click Application  
  → Traverse `CONTAINS` → Components
- Double-click Component  
  → Traverse `CALLS / READS / WRITES`

No hard-coded hierarchy.  
**Only relationships.**

---

### 6.2 Context Preservation

During drill-down:
- Origin node retained
- Traversal path remembered
- Filters applied dynamically

This allows:
- Breadcrumb navigation
- “Why am I seeing this?”
- Backtracking impact paths

---

## 7. Views as Projections (NOT DATA)

Examples of views:
- C4 diagrams
- Org dependency maps
- Data flow diagrams
- Risk heatmaps

All views:
- Query the same graph
- Apply layout + filters
- Never store separate truth

---

## 8. Impact & Blast Radius Analysis

Impact analysis is a **graph traversal problem**.

Example:
- Start node: Application A
- Traverse outgoing dependencies
- Stop at org boundary
- Highlight critical paths

Supports:
- Change risk assessment
- Failure propagation
- Compliance exposure

---

## 9. Graph Evolution Rules

1. Nodes are rarely deleted
2. Relationships expire, not vanish
3. Versions supersede, not overwrite
4. History is immutable
5. Future states are first-class

---

## 10. What This Enables (Why This Matters)

With this graph:
- Enterprise becomes **navigable**
- Architecture becomes **explainable**
- Governance becomes **evidence-based**
- Change becomes **simulatable**
- Diagrams stop lying

---

## What This Graph Is NOT

- Not a CMDB
- Not a static EA repository
- Not code-only dependency graph
- Not a documentation store

---

## Status

This document defines the **canonical Enterprise Graph Model**.

All:
- Capabilities
- Features
- APIs
- Diagrams
- Analytics

**must be derived from this graph**.
