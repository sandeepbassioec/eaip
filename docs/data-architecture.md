🗄️ Data Architecture – High Level (Logical + Physical)
1️⃣ Core Principles (Non-Negotiable)

Data follows bounded contexts

No shared databases across contexts

Events are the source of integration

Read ≠ Write models

Audit is append-only

Tenant isolation by design

2️⃣ Logical Data Domains
A. Transactional Metadata (Authoritative)

Used for writes + invariants.

Examples

Workspaces

Applications

ADRs

Diagrams (metadata)

Subscriptions

Characteristics

Strong consistency

Versioned records

Referential integrity inside context only

B. Relationship & Dependency Data

Used for impact analysis & blast radius.

Examples

App → App dependencies

Integration graphs

Capability mappings

Characteristics

Graph-oriented

Traversal-heavy

Derived from events

C. Immutable Event & Audit Data

Used for compliance & traceability.

Examples

Domain events

Webhook deliveries

Access changes

Characteristics

Append-only

Never updated

Replayable

D. Diagram & Artifact Objects

Used for large payloads & versioning.

Examples

Diagram models

Snapshots

Exports

Characteristics

Object storage

Content-addressed

Versioned

E. Read Models & Analytics

Used for dashboards & search.

Examples

Portfolio views

Risk heatmaps

Activity feeds

Characteristics

Eventually consistent

Rebuildable

Optimized for queries

---
| Logical Need           | Storage Type    |
| ---------------------- | --------------- |
| Transactional metadata | Relational DB   |
| Relationships          | Graph DB        |
| Events & audit         | Append-only log |
| Diagrams & blobs       | Object storage  |
| Search & dashboards    | Indexed store   |

4️⃣ Multi-Tenancy Data Isolation
Supported Isolation Levels
Level 1: Logical (Default)

Tenant ID on every record

Query enforcement

Cost-efficient

Level 2: Physical (Optional / BYOC)

Separate databases

Separate storage buckets

Regulatory-grade isolation

Both models use same schema + same code

5️⃣ Write vs Read Model (CQRS)
Write Path
API → Application Service → Aggregate → Event

Validates invariants

Publishes domain events

Minimal queries

Read Path
Event → Projector → Read Model → UI / API

Optimized for performance

Rebuildable anytime

No business logic

6️⃣ Event as the Spine of Data

All non-local data movement happens via events.

Used For

Read model updates

Graph population

Audit logging

External notifications

Analytics ingestion

❗ No direct cross-context DB reads allowed

7️⃣ Data Versioning Strategy
Records

Explicit version fields

Optimistic concurrency

Events

Immutable

Versioned schemas

Diagrams

Snapshot per version

Diffable

8️⃣ Data Retention & Compliance
Retention Policies

Workspace configurable

Compliance-driven

Guarantees

Audit data is never mutated

Historical decisions preserved

Full traceability for:

Who

What

When

Why (ADR linkage)

9️⃣ Backup, Restore & Recovery
Backups

Automated

Environment-specific

Tenant-aware

Recovery

Point-in-time for transactional data

Event replay for read models

Diagram restore via object versions

🔒 Forbidden Data Anti-Patterns

❌ Shared database across contexts
❌ Cross-context joins
❌ Updating audit records
❌ Using read models for writes
❌ Storing secrets in domain data

✅ Outcome

With this data architecture:

Platform scales cleanly

Auditors are happy

Multi-cloud works

BYOC is safe

No future rewrite needed
