# Data Storage, Persistence & Graph Scaling Strategy

## Purpose

This document defines **how the Enterprise Graph is persisted, queried, scaled,
and evolved over time** while remaining:
- Cloud-neutral
- Enterprise-grade
- Audit-safe
- Performant at scale

The goal is **one canonical graph** with **multiple optimized storage paths** —
without fragmenting truth.

---

## Core Principles

1. **One logical graph, multiple physical stores**
2. **Read-optimized without write chaos**
3. **Temporal data is first-class**
4. **History is immutable**
5. **Scale by partitioning, not by forking**
6. **Storage choices are replaceable**

---

## 1. Logical Data Model (Non-Negotiable)

### 1.1 Canonical Graph Model

The platform operates on a **logical property graph**:

- Nodes (typed, attributed)
- Relationships (typed, directional, attributed)
- Temporal properties (`validFrom`, `validTo`, `observedAt`)
- Source metadata (manual / observed / derived)
- Confidence score

> **Rule:**  
> Storage technology must conform to this model — not the other way around.

---

## 2. Physical Storage Strategy (Polyglot by Design)

### 2.1 Storage Layers

| Layer | Purpose | Characteristics |
|-----|--------|----------------|
| **Graph Store** | Relationships & traversals | Fast hops, deep traversals |
| **Relational Store** | Metadata & governance | Strong consistency |
| **Search Index** | Text & document search | Full-text, faceted |
| **Object Store** | Diagrams & artifacts | Immutable blobs |
| **Event Store** | Change history | Append-only |

Each layer serves a **specific access pattern**.

---

## 3. Graph Store Strategy

### 3.1 Graph Store Responsibilities
- Node/edge storage
- Multi-hop traversals
- Impact & blast-radius analysis
- Path queries (bounded)

### 3.2 Scale Model
- Partition by **Enterprise / Tenant**
- Further partition by **Organization** if required
- No cross-tenant joins

### 3.3 Technology Neutrality
Supported implementations may include:
- Native graph databases
- Graph layers over relational stores
- Managed graph services (cloud)

> **The platform depends on graph semantics, not a specific vendor.**

---

## 4. Relational Store Strategy

### 4.1 What Lives Here
- Tenancy & identity mappings
- Governance rules
- Policies & approvals
- Capability flags
- Configuration

### 4.2 Why Relational
- Strong consistency
- Transactions for governance
- Simpler migrations
- Audit alignment

---

## 5. Search & Indexing Strategy

### 5.1 Search Use Cases
- Document search (MD, Word, PDF)
- Node & relationship lookup
- Cross-cutting queries (e.g., “all ADRs touching Kafka”)

### 5.2 Index Characteristics
- Near real-time indexing
- Tenant-scoped
- Role-filtered results

Search is **derivative**, never authoritative.

---

## 6. Object Storage (Artifacts & Diagrams)

Used for:
- Auto-generated diagrams
- Imported documents
- Evidence attachments
- Snapshots

Characteristics:
- Immutable objects
- Content-addressed
- Versioned

---

## 7. Event & Change History (CRITICAL)

### 7.1 Append-Only Event Store

Every graph mutation produces an event:
- Node created/updated
- Relationship added/expired
- Policy applied
- Approval recorded

Events are:
- Immutable
- Time-stamped
- Tenant-scoped

---

### 7.2 Why This Matters
Enables:
- Audit replay
- Time travel views
- Debugging & forensics
- Safe forward-only migrations

---

## 8. Temporal & Versioning Strategy

### 8.1 No Destructive Updates

- Nodes are rarely deleted
- Relationships expire (`validTo`)
- Versions supersede, not overwrite

---

### 8.2 Time-Based Queries

Supported queries:
- “Show architecture as of date X”
- “Compare Q1 vs Q4”
- “What changed since last release?”

Time is **queryable**, not inferred.

---

## 9. Write Model vs Read Model

### 9.1 Write Model
- Strict validation
- Governance checks
- Approval workflows
- Event emission

### 9.2 Read Models
- Optimized projections
- Cached views
- Pre-aggregated insights

Read models are **rebuildable** from events.

---

## 10. Scaling Characteristics

### 10.1 Horizontal Scaling
- Read-heavy workloads scale horizontally
- Write paths remain controlled

### 10.2 Graph Traversal Limits
- Depth limits enforced
- Pagination mandatory
- Cost-based traversal guards

This prevents “graph explosions”.

---

## 11. Consistency Model (Honest & Explicit)

- **Governance & approvals:** strong consistency
- **Graph reads:** near-real-time
- **Telemetry overlays:** eventually consistent

Consistency expectations are **documented**, not assumed.

---

## 12. Backup, Restore & Disaster Recovery

- Event store = ultimate backup
- Periodic snapshots
- Tenant-isolated restore
- BYOC / On-Prem customer-controlled backups

---

## 13. On-Prem & Air-Gapped Considerations

- Local storage only
- No external dependencies
- Manual snapshot export/import
- Offline rebuild supported

---

## 14. What This Strategy Avoids

- Single-database overload
- Graph-as-document-store abuse
- Hard vendor lock-in
- Destructive schema migrations
- Unbounded traversals

---

## Outcome

With this strategy:
- The Enterprise Graph scales safely
- History is preserved
- Audits are reliable
- Performance remains predictable
- Cloud and on-prem both work

---

## Status

This document defines the **authoritative persistence and scaling strategy**.

All storage implementations and migrations **must conform** to this model.
