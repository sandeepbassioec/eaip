# Enterprise Graph Schema & Query Model

## Purpose

This document defines the **concrete technical model** of the
**Enterprise Graph** that underpins EAVIP.

It answers:
- What nodes exist?
- What relationships exist?
- How time and versions are modeled?
- How queries are expressed safely?
- What engineers implement first?

This is the **engineering contract** for the platform core.

---

## Core Principle (Reaffirmed)

> **There is one logical graph.  
> Storage and query engines must conform to it.**

---

## 1. Graph Modeling Paradigm

EAVIP uses a **property graph model** with:

- Typed nodes
- Typed, directed relationships
- Properties on both nodes and relationships
- Temporal validity
- Source attribution

This model supports:
- Architecture intent
- Runtime observations
- Governance overlays
- Time-based analysis

---

## 2. Core Node Types (Authoritative)

### 2.1 Structural Nodes

| Node Type | Description |
|---------|-------------|
| Enterprise | Root tenant |
| Organization | Business / legal unit |
| Domain | Logical grouping |
| Application | Deployable system |
| Component | Runtime unit / service |
| Interface | API / event contract |

---

### 2.2 Data & Integration Nodes

| Node Type | Description |
|---------|-------------|
| DataEntity | Logical data concept |
| Dataset | Physical data store |
| Event | Domain / integration event |
| ExternalSystem | Third-party system |
| Vendor | External provider |

---

### 2.3 Governance & Control Nodes

| Node Type | Description |
|---------|-------------|
| Policy | Governance rule |
| Control | Compliance control |
| Risk | Identified risk |
| Decision | ADR / approval |
| Requirement | Functional / NFR |

---

### 2.4 Platform & Infrastructure Nodes

| Node Type | Description |
|---------|-------------|
| CloudProvider | AWS / Azure / GCP |
| Environment | Dev / QA / Prod |
| DeploymentUnit | Runtime deployment |
| Region | Physical / logical location |

---

## 3. Core Relationship Types

### 3.1 Structural Relationships

| Relationship | Meaning |
|-------------|--------|
| CONTAINS | Hierarchical ownership |
| OWNS | Accountability |
| IMPLEMENTS | Requirement realization |

---

### 3.2 Dependency Relationships

| Relationship | Meaning |
|-------------|--------|
| CALLS | Synchronous dependency |
| EMITS | Event producer |
| CONSUMES | Event consumer |
| READS_FROM | Data access |
| WRITES_TO | Data mutation |

---

### 3.3 Governance Relationships

| Relationship | Meaning |
|-------------|--------|
| GOVERNED_BY | Policy application |
| VIOLATES | Rule breach |
| APPROVED_BY | Explicit approval |
| MITIGATED_BY | Risk control |

---

## 4. Temporal & Versioning Model (CRITICAL)

### 4.1 Temporal Properties (Standard)

Every node and relationship supports:

```json
{
  "validFrom": "timestamp",
  "validTo": "timestamp | null",
  "observedAt": "timestamp | null",
  "source": "manual | observed | derived",
  "confidence": 0.0 – 1.0
}
```
Rules:

No hard deletes

Expiration instead of mutation

History always queryable

5. Write Model (Strict)

All mutations must:

Validate schema

Check permissions

Apply governance rules

Emit immutable events

Update read models asynchronously

No direct graph writes from UI or plugins.

6. Read & Query Model (Safe by Design)
6.1 Query Characteristics

Read-only

Depth-limited

Relationship-filtered

Time-context aware

Tenant-scoped

6.2 Example Query Intents

“Show all downstream dependencies of Application X”

“What breaks if Component Y is removed?”

“Which orgs consume data owned by Org A?”

“Show architecture as of last quarter”

7. Graph Query Abstraction (IMPORTANT)

The platform exposes:

Intent-based queries

NOT raw graph query language

Example (conceptual):
GET /graph/impact?node=Application:X&depth=3&time=now

This avoids:

Vendor lock-in

Unsafe traversals

Accidental data exposure

8. Performance & Safety Guards

Max traversal depth enforced

Node count caps per query

Pagination mandatory

Cost-based query rejection

These prevent “graph explosion” scenarios.

9. Storage Mapping (Abstract)

Logical graph can be backed by:

Native graph DB

Relational + adjacency tables

Hybrid graph layers

The logical contract does not change.

10. What Engineers Build First (Execution Order)

Core node & relationship schemas

Temporal support

Event emission on change

Read-only query APIs

Minimal write commands

Simple visualization consumption

Everything else builds on this.

What This Avoids

Overloaded schema

Premature optimization

Query language exposure

Destructive updates

Hidden coupling

Outcome

With this model:

Engineers have a clear contract

Architects retain semantic clarity

Governance remains enforceable

Scale is predictable

Future evolution is safe

Status

This document defines the authoritative Enterprise Graph schema and query model.

All platform engineering must conform to this contract.

---
