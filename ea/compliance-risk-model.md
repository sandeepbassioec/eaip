# Compliance, Risk & Regulatory Mapping
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines how **compliance, risk, and regulatory obligations**
are modeled, evaluated, and governed within EAVIP.

It answers:
- How compliance requirements map to architecture
- How risk is identified, assessed, and tracked
- How regulatory evidence is preserved over time

> Compliance is not a checklist.  
> Compliance is **continuous alignment between intent and reality**.

---

## Problem Statement

In most enterprises:
- Compliance evidence is scattered across documents
- Risk is assessed manually and periodically
- Regulatory violations are discovered too late

The root cause is lack of **architectural traceability**.

---

## Design Goals

1. Make compliance architecture-aware
2. Make risk visible and explainable
3. Preserve evidence over time
4. Support multiple regulations simultaneously
5. Avoid compliance-by-documentation

---

## Options Considered

### Option A: External GRC Tool Only
- Compliance tracked outside architecture systems

**Pros**
- Specialized tooling
- Familiar to auditors

**Cons**
- No architectural context
- Manual reconciliation
- High drift risk

---

### Option B: Static Compliance Documentation
- Policies and checklists

**Pros**
- Simple
- Low tooling cost

**Cons**
- Quickly outdated
- Not enforceable

---

### Option C: Architecture-Embedded Compliance (Chosen)

Compliance and risk modeled directly against architecture entities.

---

## Final Decision (Locked)

EAVIP will treat **Compliance and Risk as first-class architectural concerns**
mapped directly to Enterprise Graph entities.

---

## Compliance Model

### Core Concepts

- **Regulation**
  - e.g., GDPR, SOC2, ISO 27001
- **Control**
  - Specific requirement within a regulation
- **Obligation**
  - What must be enforced or proven
- **Evidence**
  - Architecture data, decisions, or runtime signals

---

### Compliance Mapping

Compliance can be mapped to:
- Enterprise
- Organization
- Application
- Component
- Data Flow
- Deployment Model

This allows:
- Partial compliance tracking
- Shared responsibility modeling
- Precise gap identification

---

## Risk Model

### Risk Categories

- Security Risk
- Operational Risk
- Compliance Risk
- Dependency Risk
- Cost Risk

---

### Risk Assessment Dimensions

Each risk is evaluated on:
- Likelihood
- Impact
- Exposure surface
- Mitigation status

Risk is **derived**, not manually declared.

---

## Continuous Risk Evaluation

Risk scores are recalculated when:
- Architecture changes
- Dependencies change
- Deployment topology changes
- New regulations are added

This enables **proactive risk detection**.

---

## Regulatory Evidence Preservation

### What Is Preserved

- Architecture state at decision time
- Associated ADRs
- Approval records
- Impact analysis snapshots

### Why This Matters

Auditors often ask:
> “What did you know at the time of decision?”

EAVIP can answer this question precisely.

---

## Trade-offs

**Pros**
- Continuous compliance visibility
- Reduced audit effort
- Explainable risk posture

**Cons**
- Higher modeling complexity
- Requires disciplined architecture capture

---

## Why This Approach Is Best

- Aligns compliance with real system design
- Eliminates document drift
- Supports long-lived regulatory requirements
- Scales across enterprises and regulations

---

## Example Scenarios

### GDPR
- Data flows crossing regions flagged
- PII handling traced to components

### SOC2
- Deployment and access models validated
- Change approval evidence preserved

---

## Closing Notes

Compliance and risk cannot be bolted on after the fact.
They must be **designed into the architecture**.

EAVIP transforms compliance from:
- Reactive audits  
to  
- Continuous architectural assurance.
