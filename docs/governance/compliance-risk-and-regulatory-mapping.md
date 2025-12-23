# Compliance, Risk & Regulatory Mapping on the Enterprise Graph

## Purpose

This document defines how **compliance requirements, regulatory obligations,
and enterprise risks** are modeled, enforced, and continuously validated
within the **Enterprise Architecture Visibility & Intelligence Platform (EAVIP)**.

It ensures that:
- Compliance is **architecturally provable**
- Risk is **contextual, not abstract**
- Audits become **graph queries**, not manual exercises
- Compliance posture remains **time-aware and explainable**

---

## Core Principles

1. **Compliance attaches to architecture, not documents**
2. **Controls are first-class graph entities**
3. **Evidence is continuous and immutable**
4. **Risk is contextual and impact-based**
5. **Compliance is time-aware**
6. **One source of truth for auditors and architects**

---

## 1. Compliance as a Graph Concept

### 1.1 Compliance Node Taxonomy

Compliance is modeled explicitly as nodes:

| Node Type | Description |
|---------|-------------|
| Regulation | Law or regulatory mandate |
| Standard | Industry standard |
| Control | Specific control requirement |
| Obligation | Enterprise-specific obligation |
| Evidence | Proof artifact |
| Risk | Identified risk |
| Mitigation | Risk treatment |

Examples:
- GDPR
- SOC 2
- ISO 27001
- PCI-DSS
- HIPAA

---

## 2. Regulation & Standard Modeling

### 2.1 Regulation Nodes

Each **Regulation** node includes:
- Jurisdiction
- Applicability criteria
- Enforcement authority
- Effective dates

---

### 2.2 Standard Nodes

Standards define:
- Control families
- Control objectives
- Maturity levels

Standards can:
- Reference regulations
- Be reused across enterprises

---

## 3. Control Modeling (CRITICAL)

### 3.1 Control Definition

A **Control** node defines:
- Control intent
- Required behavior
- Validation method
- Evidence expectations

Controls are **technology-agnostic**.

---

### 3.2 Control Attachment

Controls attach to:
- Applications
- Components
- Data entities
- Data flows
- Cloud resources
- External dependencies

Relationship types:
- ENFORCED_BY
- SATISFIES
- VIOLATES
- EVIDENCED_BY

---

## 4. Data-Centric Compliance (VERY IMPORTANT)

### 4.1 Data Protection Obligations

For each **DataEntity / Dataset**:
- Applicable regulations
- Residency constraints
- Retention requirements
- Consent requirements

---

### 4.2 Data Flow Compliance

Every data flow is validated for:
- Cross-border transfer legality
- Encryption requirements
- Data minimization
- Purpose limitation

Violations are shown:
- Directly on data flow diagrams
- With jurisdictional context

---

## 5. Cloud & Infrastructure Compliance

### 5.1 Cloud Compliance Modeling

Cloud entities modeled:
- CloudAccount
- Region
- ManagedService

Controls attach to:
- Region restrictions
- Service usage
- Network isolation
- Encryption standards

---

### 5.2 Multi-Cloud & BYOC Compliance

Supports:
- SaaS model
- BYOC model
- Hybrid model

Each deployment context has:
- Independent compliance posture
- Shared governance rules

---

## 6. External & Third-Party Compliance

### 6.1 Vendor Compliance Modeling

External dependencies include:
- Certification claims
- Contractual obligations
- Data handling commitments

---

### 6.2 Third-Party Risk

Risk surfaced when:
- Sensitive data flows externally
- External SLA < internal requirement
- Certification gaps exist

---

## 7. Risk Modeling (NOT JUST CHECKLISTS)

### 7.1 Risk Node Definition

A **Risk** node includes:
- Description
- Likelihood
- Impact
- Scope
- Owner
- Review cadence

---

### 7.2 Risk Relationships

Risks attach to:
- Architecture elements
- Controls
- Dependencies
- Data flows

Relationship types:
- CAUSED_BY
- MITIGATED_BY
- ACCEPTED_BY

---

## 8. Continuous Compliance Validation

### 8.1 Validation Triggers

Validation runs on:
- Architecture changes
- New dependencies
- Cloud drift
- Time-based reviews

---

### 8.2 Evidence Collection

Evidence can be:
- Automated (cloud config, runtime signals)
- Manual (attestations, reviews)
- Imported (audit reports)

Evidence is:
- Immutable
- Time-stamped
- Linked to controls

---

## 9. Compliance Over Time (AUDIT-READY)

### 9.1 Time-Aware Compliance

Supports:
- “Show compliance posture on date X”
- “What changed since last audit?”
- “Which controls degraded over time?”

---

### 9.2 Audit Replay

Auditors can:
- Navigate architecture at audit time
- See applicable controls
- See evidence attached
- Trace decisions and exceptions

---

## 10. Compliance Views & Dashboards

### 10.1 Architect View
- Control coverage gaps
- High-risk flows
- Drift alerts

### 10.2 Compliance Officer View
- Regulation coverage
- Evidence completeness
- Open risks

### 10.3 Executive View
- Compliance posture
- Risk exposure
- Trend indicators

---

## 11. Exception & Risk Acceptance Handling

- Exceptions are explicit
- Time-bound
- Reviewed periodically
- Visible on architecture diagrams

No hidden risk acceptance.

---

## What This Model Avoids

- Spreadsheet-based compliance
- Manual evidence chasing
- Point-in-time audits only
- Detached risk registers
- Tool-specific silos

---

## Outcome

With this model:
- Compliance is **provable**
- Risk is **contextual**
- Audits are **predictable**
- Architecture and regulation are **aligned**

---

## Status

This document defines the **authoritative compliance, risk, and regulatory model**.

All compliance features, validations, and audit workflows **must derive from the Enterprise Graph**.
