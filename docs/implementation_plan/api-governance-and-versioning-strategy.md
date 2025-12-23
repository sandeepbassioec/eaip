docs/platform/api-governance-and-versioning-strategy.md

# API Governance & Versioning Strategy

## Purpose

This document defines the authoritative API governance and versioning strategy
for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It ensures that:
- APIs remain stable as the platform evolves
- Consumers are protected from breaking changes
- Governance is enforced without blocking delivery
- APIs reflect architectural intent, not implementation details

This is the contract between EAVIP and all internal and external consumers.

---

## API Governance Principles (Locked)

1. APIs are long-lived contracts, not internal conveniences
2. Breaking changes are exceptional, never routine
3. Versioning is explicit and predictable
4. Governance applies equally to internal and external APIs
5. Read and write responsibilities are clearly separated
6. Architecture truth is never leaked through APIs

---

## API Classification

EAVIP APIs are classified into the following categories:

- Command APIs
- Query APIs
- Integration APIs
- Event APIs

Each category has different governance and stability guarantees.

---

## Command APIs

Purpose:
- Mutate platform state through governed workflows

Characteristics:
- Explicit intent (create, propose, approve)
- Always go through governance checks
- Idempotent where applicable

Rules:
- Commands are never backward-incompatible within a major version
- Commands do not return domain internals
- Commands may evolve via additive fields only

---

## Query APIs

Purpose:
- Read-only access to architecture views and reports

Characteristics:
- No side effects
- Optimized for consumption
- Derived from the Enterprise Graph

Rules:
- Queries never expose graph query languages
- Queries may add new fields without version bump
- Removal or semantic change requires new version

---

## Integration APIs

Purpose:
- Enable external systems to interact with EAVIP

Examples:
- CI/CD systems
- Governance tools
- External reporting platforms

Rules:
- Always versioned
- Backward compatibility guaranteed for supported versions
- Clear deprecation timelines published

---

## Event APIs

Purpose:
- Publish architecture and governance events to subscribers

Characteristics:
- Asynchronous
- Immutable payloads
- Schema-defined events

Rules:
- Event schemas are versioned independently
- Old event versions continue to be published during deprecation window
- Consumers choose which versions to subscribe to

---

## Versioning Strategy

APIs follow semantic versioning:

- Major: Breaking changes
- Minor: Backward-compatible additions
- Patch: Bug fixes and clarifications

The version is part of the API path or header.

---

## Deprecation Policy (Non-Negotiable)

- Deprecation notice provided in advance
- Deprecation reason clearly documented
- Minimum support window defined
- Removal requires explicit governance approval

Silent breaking changes are forbidden.

---

## API Lifecycle States

Every API endpoint has an explicit lifecycle state:

- Experimental
- Stable
- Deprecated
- Retired

Lifecycle state is visible in documentation and metadata.

---

## Governance Enforcement

API changes require:
- Design review
- Compatibility analysis
- Impact assessment
- Explicit approval for breaking changes

Automated checks enforce:
- Versioning rules
- Backward compatibility
- Documentation completeness

---

## Security & Access Control

- APIs secured via OAuth2 / OIDC
- Scopes defined per API category
- Tenant isolation enforced at API boundary
- Sensitive data never exposed by default

---

## Documentation Requirements

For every API:
- Purpose and scope
- Version and lifecycle state
- Request and response schema
- Error model
- Examples
- Deprecation notes (if applicable)

Documentation is mandatory for release.

---

## What This Strategy Prevents

- Accidental breaking changes
- Consumer lock-in to internals
- Uncontrolled API sprawl
- Inconsistent integration behavior
- Governance bypass

---

## Outcome

With this governance and versioning strategy:
- APIs remain trustworthy
- Integrations scale safely
- Platform evolution is controlled
- Consumer confidence is maintained

---

## Status

This document defines the authoritative API governance and versioning strategy
for EAVIP. All API design and changes must conform to this strategy.
