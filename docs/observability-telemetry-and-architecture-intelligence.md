# Observability, Telemetry & Architecture Intelligence Signals

## Purpose

This document defines how **runtime observability signals** (metrics, traces,
logs, topology) enrich the **Enterprise Graph** to produce **Architecture
Intelligence** — not dashboards for dashboards’ sake.

The platform answers:
- What is **actually** talking to what?
- Which dependencies are **hot paths**?
- Where is **architecture drift** emerging at runtime?
- Which components are **business-critical in practice**, not on paper?

---

## Core Principles

1. **Signals enrich the graph; they don’t replace it**
2. **Architecture insight > raw telemetry**
3. **Noise is filtered at ingestion**
4. **Time is a first-class dimension**
5. **Vendor-neutral by default**
6. **Runtime never overrides intent silently**

---

## 1. Telemetry Sources (WHAT we ingest)

### 1.1 Metrics
- Request rate, latency, errors
- Resource utilization
- Throughput

Used to infer:
- Critical paths
- Saturation risks
- De-facto importance

---

### 1.2 Distributed Traces
- Service-to-service calls
- API fan-in / fan-out
- Cross-boundary interactions

Used to infer:
- Actual dependency graph
- Hidden integrations
- Latency propagation paths

---

### 1.3 Logs (Selective)
- Security-relevant events
- Integration failures
- Contract violations

Used to:
- Validate governance
- Explain incidents
- Attach evidence

---

### 1.4 Topology & Service Maps
- Kubernetes service maps
- Cloud network flows
- Mesh / gateway routes

Used to:
- Discover runtime architecture
- Validate deployment diagrams

---

## 2. Vendor-Neutral Ingestion Model

Supported sources (pluggable):
- OpenTelemetry
- Cloud-native APIs (AWS, Azure, GCP)
- Existing APMs (via adapters)
- Network telemetry (flow logs)

**Rule:**  
EAVIP does not become an APM.  
It **consumes signals**, it does not store raw telemetry forever.

---

## 3. Signal Normalization & Confidence

Every signal is normalized into:
- Node (Application / Component)
- Relationship (CALLS / DEPENDS_ON)
- Attributes:
  - Frequency
  - Latency percentile
  - Error rate
  - Observation window
  - Confidence score

Signals are tagged as:
- OBSERVED
- DERIVED
- CORROBORATED

---

## 4. Runtime vs Intended Architecture

### 4.1 Runtime Overlay

Observed relationships overlay on:
- Intended architecture
- Approved ADRs
- Governance rules

Visual cues:
- Solid = intended + observed
- Dashed = intended only
- Red = observed only (drift)

---

### 4.2 Drift Detection from Telemetry

Detected automatically:
- New undocumented calls
- Deprecated APIs still in use
- Cross-org calls bypassing gateways
- Sensitive data paths at runtime

All drift:
- Time-stamped
- Source-attributed
- Explainable

---

## 5. Architecture Intelligence Signals (THE VALUE)

Telemetry is converted into **architecture-level insights**.

### 5.1 Criticality Scoring
- Components ranked by:
  - Traffic share
  - Dependency fan-in
  - Failure blast radius

Shows:
- “Architecturally critical” vs “theoretically important”

---

### 5.2 Hot Path Identification
- Runtime hot paths across apps/orgs
- Used for:
  - Resilience design
  - Capacity planning
  - Modernization prioritization

---

### 5.3 Dependency Health
- Stable vs volatile dependencies
- Chattiness detection
- Latency amplification

---

## 6. Time-Aware Architecture Evolution

Telemetry is always time-scoped:
- Last hour
- Last release
- Last quarter

Enables:
- Before/after comparisons
- Release impact analysis
- Long-term trend detection

---

## 7. Governance & Security Signals from Runtime

Runtime signals can trigger:
- Security boundary violations
- Data flow violations
- Policy breaches

But:
> **Runtime signals never auto-approve architecture changes**

They:
- Propose
- Highlight
- Explain

Humans decide.

---

## 8. Storage & Retention Strategy

- Raw telemetry: short retention (external systems)
- Aggregated signals: retained
- Architecture insights: retained long-term

This keeps:
- Costs low
- Signal high
- History meaningful

---

## 9. Views & Visualizations (Auto-Generated)

Telemetry-powered views:
- Runtime dependency map
- Hot path overlays
- Criticality heatmaps
- Drift timelines

All views derive from the **same Enterprise Graph**.

---

## 10. What This Avoids

- Becoming another monitoring tool
- Duplicating APM dashboards
- Long-term raw log storage
- Vendor lock-in
- Architecture-by-metrics-only

---

## Outcome

With this model:
- Architecture reflects **reality**
- Drift is detected **early**
- Critical paths are **obvious**
- Decisions are **data-informed**
- Telemetry becomes **strategic**

---

## Status

This document defines the **authoritative observability and architecture
intelligence model** for EAVIP.

All telemetry ingestion, analysis, and visualizations **must conform** to this model.
