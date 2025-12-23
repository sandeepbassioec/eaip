# Diagram Interaction & Inline Creation Rules

## Purpose

This document defines the **authoritative rules for interacting with diagrams**
in the Enterprise Architecture Visibility & Intelligence Platform (EAVIP),
including **inline creation of entities directly from diagrams**.

It explicitly locks the requirement that:
> Users can create architecture elements directly from diagrams,
> with explicit confirmation and controlled behavior.

This is the **diagram interaction contract** for UX, frontend, backend, and governance.

## Core Interaction Principles (Locked)

1. Diagrams are interactive, not static
2. No diagram action mutates the graph silently
3. Inline actions always require explicit user intent
4. Diagram interactions follow the same governance rules as APIs
5. Creation from diagrams improves speed without reducing control

## Inline Creation Requirement (LOCKED)

When a user performs an action directly on a diagram
(e.g. drawing a component, project, application, or connection):

➡️ **The system MUST show a confirmation popup**

This requirement is **non-optional and globally enforced**.

## Inline Creation Modes (Authoritative – TWO TYPES)

### Type 1: Add Existing Entity

Used when:
- The drawn element matches an existing entity
- The user wants to reuse something already defined

Popup must ask:
- “This entity already exists. Do you want to link it to this context?”

Options:
- Link existing entity
- Cancel

Rules:
- No duplication allowed
- Relationship is proposed, not auto-applied
- Governance applies if required

## Type 2: Create New Entity

Used when:
- The entity does not exist
- The user intends to define something new

Popup must ask:
- “Do you want to create a new entity?”

Required inputs:
- Entity type (Application / Component / Project / etc.)
- Name
- Owning organization
- Optional metadata (criticality, lifecycle)

Rules:
- Creates a proposal, not an immediate graph mutation
- Follows standard governance workflow
- Appears as “pending” in diagrams until approved

## Popup Behavior Rules

- Popup is mandatory
- Popup blocks further diagram interaction
- No default auto-selection
- Cancel always leaves graph unchanged
- User intent must be explicit

## Diagram Creation Scope

Inline creation is allowed for:
- Organizations
- Applications
- Components
- Projects / Initiatives
- Dependencies (as proposals)

Inline creation is NOT allowed for:
- Policies
- Security controls
- Compliance rules
- System-level configuration

## Visual State Handling

While pending approval:
- Entities appear in diagrams with “pending” state
- Distinct visual treatment (dashed border / muted color)
- Tooltip explains approval status

Rejected items:
- Are removed from active view
- Remain visible in audit/history views

## Governance Integration

Inline creation:
- Uses the same proposal engine
- Triggers the same validation rules
- Requires the same approvals
- Produces the same audit trail

There is **no fast path** that bypasses governance.

## Audit & Traceability

For every inline action, the system records:
- Who initiated it
- From which diagram
- Timestamp
- Confirmation choice
- Final decision outcome

Diagram-driven changes are fully auditable.

## What This Model Avoids

- Silent architecture changes
- Accidental duplication
- Diagram-only truth
- Governance bypass via UX
- Confusion between drawing and modeling

## Outcome

With this interaction model:
- Diagrams become productive tools
- Speed and safety coexist
- User intent is always explicit
- Governance remains intact
- Architects trust what they see

## Status

This document defines the **authoritative diagram interaction and inline creation rules**.
All diagram behavior and UX flows must conform to this model.
