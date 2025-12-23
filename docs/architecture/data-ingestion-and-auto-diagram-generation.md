# Data Ingestion & Auto-Diagram Generation

## Purpose

This document defines the **authoritative ingestion model** for EAVIP and how
**truthful diagrams are auto-generated** from ingested data.

It explains:
- What data can be ingested
- How ingestion is validated and governed
- How the Enterprise Graph is updated safely
- How diagrams are generated automatically (never manually)

This is the **data ingestion and visualization contract** for the platform.

## Core Ingestion Principles (Locked)

1. Ingestion never bypasses governance
2. All ingested data is attributable to a source
3. Confidence is explicit, never assumed
4. Diagrams are generated, not drawn
5. Conflicts are surfaced, not auto-resolved
6. Manual input and automated input coexist safely

## Ingestion Sources (Authoritative)

EAVIP supports multiple ingestion sources:

- Manual UI input
- REST APIs
- CI/CD pipelines
- Code repositories (metadata only)
- Infrastructure definitions (IaC metadata)
- Observability tools (future phase)
- External catalogs (future phase)

Each source is treated as **untrusted until validated**.

## Ingestion Modes

### Manual Ingestion
- Architects explicitly model entities
- Highest confidence
- Governance-first

### Assisted Ingestion
- Tooling suggests entities or dependencies
- Requires human confirmation
- Confidence marked as “assisted”

### Automated Ingestion
- System-generated metadata
- Lowest default confidence
- Always reviewable and reversible

## Ingestion Pipeline (Authoritative Flow)

Source Input  
→ Normalization  
→ Schema Validation  
→ Policy Validation  
→ Proposal Creation  
→ Approval (if required)  
→ Graph Update  
→ Event Emission  
→ Diagram Regeneration  

No step is optional.

## Normalization Rules

Incoming data is normalized into:
- Canonical node types
- Canonical relationship types
- Standard property names
- Explicit timestamps
- Explicit source attribution

No raw external schema is stored directly.

## Validation Rules

Every ingestion undergoes:
- Schema validation
- Tenant isolation validation
- Relationship legality checks
- Data sensitivity checks
- Duplication detection

Invalid data is rejected with explainable errors.

## Conflict Handling

Conflicts include:
- Duplicate applications
- Conflicting dependencies
- Mismatched ownership
- Inconsistent data classification

Conflict resolution:
- Never automatic
- Always visible
- Requires human decision or policy override

## Confidence Model

Each ingested element carries:
- Source
- Confidence score
- Observation timestamp

Confidence is used to:
- Influence visualization emphasis
- Drive review workflows
- Support trust decisions

## Auto-Diagram Generation Model

Diagrams are generated from:
- Enterprise Graph
- Time context
- User role
- View level (Enterprise / Org / App / Component)

There is **no diagram state stored independently**.

## Supported Diagram Types (Phase-Wise)

### Phase-1 (MVP)
- Enterprise overview
- Organization application map
- Application container diagram
- Component dependency view

### Phase-2+
- C4 context & container
- Data flow diagrams
- Integration diagrams
- ER-style data views
- Security boundary overlays

## Diagram Generation Rules

- Layout is deterministic
- No manual node positioning
- Filters affect visibility, not truth
- Time context always respected
- Policies can suppress or annotate elements

## Regeneration Triggers

Diagrams regenerate when:
- Graph changes are approved
- Time context changes
- Filters change
- Role context changes

Regeneration is fast and stateless.

## Governance Interaction

If ingestion introduces:
- New dependencies
- Sensitive data flows
- Cross-org integrations

Then:
- A proposal is created
- Governance workflow applies
- Diagrams show “pending” state until approval

## Audit & Traceability

For every ingested element:
- Source is known
- Confidence is visible
- Approval history is recorded
- Changes are versioned

Nothing is silent.

## What This Model Avoids

- Stale diagrams
- Hand-drawn inconsistencies
- Hidden automation
- Blind trust in tools
- Data ingestion chaos

## Outcome

With this ingestion and auto-diagram model:
- Architecture stays truthful
- Automation helps but never lies
- Diagrams always reflect reality
- Trust is measurable
- Scale does not reduce clarity

## Status

This document defines the **authoritative data ingestion and auto-diagram generation model**.
All ingestion mechanisms and visualizations must conform to this design.
