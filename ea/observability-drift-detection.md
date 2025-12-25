# Observability, Telemetry & Architecture Drift Detection
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines how EAVIP implements **observability and telemetry**
to detect **architecture drift** between *intended design* and *runtime reality*.

It explains:
- What observability means at an architecture level
- How telemetry feeds the Enterprise Architecture Graph
- How drift is detected, classified, and explained
- Why drift detection is critical for long-term architectural health
- How this works without disrupting production systems

This document acts as a **reference model** for architecture intelligence.

---

## Core Principle (Locked)

**If architecture intent is not continuously verified against reality,
it will inevitably drift.**

Drift is not a failure — **undetected drift is**.

---

## What Is Architecture Observability

Architecture observability answers:
- What is actually running?
- How systems are really interacting?
- Where reality diverges from design?
- When did the divergence start?
- What is the impact?

This goes beyond logs and metrics — it is **structural observability**.

---

## Intended vs Observed Architecture

### Intended Architecture
- Defined by architects
- Captured via models, diagrams, ADRs
- Represents *how things should work*

### Observed Architecture
- Derived from runtime signals
- Telemetry, traces, configs
- Represents *how things actually work*

EAVIP models both **explicitly**.

---

## Telemetry Sources (Non-Invasive)

Telemetry is collected via:
- Service traces
- Network flow logs
- API gateway logs
- CI/CD metadata
- Configuration snapshots
- Dependency manifests

No code instrumentation is mandatory initially.

---

## Telemetry Ingestion Strategy

Rules:
- Read-only ingestion
- No mutation of source systems
- Sampling-first approach
- Opt-in per capability

This ensures:
- Safety
- Trust
- Incremental adoption

---

## Architecture Signals Captured

Examples:
- New service-to-service calls
- Unexpected data flows
- Unauthorized integrations
- Deployment topology changes
- Runtime dependency changes

Each signal is timestamped and contextualized.

---

## Drift Detection Types

### Structural Drift
- New dependencies
- Removed integrations
- Bypassed services

### Security Drift
- Trust boundary violations
- Unauthorized access paths
- Policy bypasses

### Deployment Drift
- Topology mismatches
- Single points of failure introduced
- Environment inconsistencies

### Governance Drift
- Decisions not recorded
- Policies bypassed
- Temporary exceptions becoming permanent

---

## Drift Classification

Drift is classified by:
- Severity (Low / Medium / High / Critical)
- Scope (Local / Cross-App / Enterprise)
- Intent (Known / Unknown)
- Duration (Transient / Persistent)

This prevents alert fatigue.

---

## Drift Explanation (Critical Feature)

Every drift must be:
- Explained in human-readable terms
- Linked to impacted entities
- Linked to missing or outdated decisions

Example:
> “Service A directly called Service C, bypassing approved Service B,
violating dependency policy DEP-004.”

---

## Drift Response Model

Drift does NOT automatically trigger enforcement.

Instead:
1. Drift detected
2. Explanation generated
3. Impact analyzed
4. Options presented
5. Human decision recorded

This preserves autonomy and trust.

---

## Feedback into TOGAF Lifecycle

Detected drift may trigger:
- Phase H (Change Management)
- Phase A (Vision Reassessment)
- Phase G (Governance Enforcement)

This keeps architecture **alive**.

---

## Visualization of Drift

Drift is visualized as:
- Overlays on diagrams
- Highlighted dependency edges
- Timeline-based change views

Visuals help humans reason faster than reports.

---

## Storage of Observability Data

Rules:
- Append-only
- Time-series aware
- Correlated with architecture entities
- Retention policies configurable

History is preserved for audit and learning.

---

## Trade-offs

**Pros**
- Early detection of issues
- Reduced surprise failures
- Strong governance signals
- Continuous alignment

**Cons**
- Requires telemetry maturity
- Additional data storage
- Interpretation effort

---

## Why This Model Works

- Non-invasive
- Incrementally adoptable
- Human-centric
- Enterprise-scale

Observability becomes **architecture intelligence**, not just ops noise.

---

## Final Mental Model

- Architecture intent defines expectation
- Telemetry defines reality
- Drift defines learning opportunity
- Governance defines response

---

## Next Step

Proceed to **Reporting, Dashboards & Executive Views**  
File: `ea/reporting-executive-views.md`
