# Governance, Validation & Architecture Drift Detection

## Purpose

This document defines how EAVIP enforces **architecture governance**,
detects **drift between intent and reality**, and provides **explainable,
actionable feedback** across:

- Inter-application dependencies
- Inter-component interactions
- Cross-organization flows
- Cloud & external dependencies
- Security, compliance, and technology standards

The system moves from **documentation** to **continuous architecture control**.

---

## Core Principles

1. **Governance is continuous, not periodic**
2. **Rules attach to the graph, not documents**
3. **Drift is detected automatically**
4. **Every violation is explainable**
5. **Governance never blocks blindly — it guides**

---

## 1. Governance Model (WHAT is governed)

### 1.1 Governance Scopes

Governance rules can apply at:

- Enterprise level
- Organization level
- Domain level
- Application level
- Component level

Rules inherit downward unless overridden.

---

### 1.2 Governed Dimensions

| Dimension | Examples |
|---------|----------|
| Architecture | Allowed patterns, layering |
| Dependencies | Who can call whom |
| Data | Ownership, sensitivity, flow |
| Technology | Approved stacks, EOL |
| Cloud | Region, service usage |
| Security | Trust boundaries, auth |
| Compliance | Regulatory controls |

---

## 2. Policy Definition Model (HOW rules are expressed)

### 2.1 Policy Structure

Each policy is defined as:

- **Scope** (where it applies)
- **Condition** (graph pattern)
- **Expectation** (what should be true)
- **Severity** (info / warn / critical)
- **Rationale** (why this exists)
- **Evidence** (what to show)

Policies are **declarative**, not procedural.

---

### 2.2 Example Policies

#### Example 1: Cross-Org Data Flow
- Condition: `TRANSFERS data across organizations`
- Expectation: `Must have data contract + approval`
- Severity: Critical

#### Example 2: Undocumented Dependency
- Condition: `OBSERVED CALL exists without INTENDED CALL`
- Expectation: `ADR required`
- Severity: Warning

#### Example 3: Deprecated Technology
- Condition: `Component DEPENDS_ON deprecated technology`
- Expectation: `Migration roadmap`
- Severity: Info

---

## 3. Validation Engine (HOW rules are evaluated)

### 3.1 Validation Triggers

Validation runs on:
- Graph changes
- New ingestion events
- Time-based schedules
- Manual review requests

---

### 3.2 Validation Mechanics

Validation is:
- Graph traversal + pattern matching
- Time-aware
- Context-preserving

Produces:
- Violations
- Warnings
- Recommendations

---

## 4. Drift Detection (INTENT vs REALITY)

### 4.1 Drift Types

| Drift Type | Description |
|----------|-------------|
| Structural | Missing / extra components |
| Dependency | Undocumented calls |
| Data | Unexpected data flows |
| Technology | Runtime vs approved stack |
| Cloud | Resource sprawl |
| Security | Boundary violations |

---

### 4.2 Drift Identification

Drift is detected by comparing:
- **INTENDED graph** (ADR, design, target)
- **OBSERVED graph** (runtime, cloud, CI/CD)

Differences are classified, not just flagged.

---

### 4.3 Drift Visualization

Drift is shown:
- Directly on diagrams
- As overlays (red / amber)
- With explainable tooltips

Users can ask:
- “When did this appear?”
- “Who approved this?”
- “What does it impact?”

---

## 5. Explainability & Evidence (WHY this matters)

Every violation links to:
- Affected nodes & edges
- Source of detection
- Related ADRs
- Related requirements
- Compliance controls

No “black box” warnings.

---

## 6. Governance Workflows (WHAT happens next)

### 6.1 Violation Lifecycle

1. Detected
2. Classified
3. Assigned
4. Acknowledged
5. Remediated or Accepted
6. Closed

---

### 6.2 Acceptance vs Remediation

- Some violations require fixes
- Some require risk acceptance
- All require **traceable decisions**

Accepted risks:
- Time-bound
- Reviewed periodically
- Visible on dashboards

---

## 7. Governance Views & Dashboards

### 7.1 Architect View
- Active violations
- Drift hotspots
- Risk trends

### 7.2 Engineering View
- Actionable fixes
- Impact analysis
- Dependency context

### 7.3 Executive View
- Governance posture
- Risk exposure
- Transformation alignment

---

## 8. Integration with Change & CI/CD

Governance signals can:
- Block deployments (optional)
- Warn pipelines
- Trigger reviews
- Update roadmaps

But:
> **Human decision always remains explicit**

---

## 9. Governance Across Cloud & Externals

### Cloud Governance
- Region restrictions
- Service allow-lists
- Network boundary enforcement

### External Dependencies
- Vendor risk tracking
- License compliance
- SLA awareness

---

## 10. What This Avoids

- Checkbox governance
- Static reviews
- Manual audits only
- Tool-enforced dogma
- Unexplainable rules

---

## Outcome

With this model:
- Architecture discipline is **continuous**
- Drift is **visible early**
- Governance is **evidence-based**
- Enterprises move **with confidence**

---

## Status

This document defines the **authoritative governance and drift detection model**.

All validation engines, policies, and dashboards **must conform** to this model.
