# Enterprise Architecture Documentation Index
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document serves as the **master index** for all enterprise architecture
artifacts related to EAVIP.

It provides:
- A single entry point for navigation
- Logical organization of documents
- Long-term discoverability
- Context preservation across time and teams

> If architecture documentation cannot be navigated easily,  
> it will not be trusted or used.

---

## How to Use This Index

- Start with **Architecture Vision** to understand intent
- Follow **Capabilities & Views** to understand structure
- Refer to **Decisions & Constraints** to understand reasoning
- Use **Roadmaps** to understand evolution
- Use **Governance & Compliance** for control and assurance

Documents are ordered in the same sequence an enterprise architect
would reason about the system.

---

## 1. Vision & Intent

These documents explain **why EAVIP exists** and what problems it solves.

- [`architecture-vision.md`](./architecture-vision.md)  
  *Overall purpose, business pain points, success criteria*

---

## 2. Capabilities & Scope

These documents describe **what EAVIP can do**, independent of technology.

- [`capability-map.md`](./capability-map.md)  
  *Core and supporting capabilities of the platform*

---

## 3. Domain & Context Structure (DDD × TOGAF)

These documents explain **how responsibilities are divided** and
**how domains interact**.

- [`bounded-contexts.md`](./bounded-contexts.md)  
  *Bounded contexts, ownership, and responsibilities*

---

## 4. Architecture Views

These documents describe the system from **different architectural lenses**.

- [`logical-architecture.md`](./logical-architecture.md)  
  *Capabilities and high-level responsibilities*

- [`application-architecture.md`](./application-architecture.md)  
  *Applications, services, and interactions*

- [`data-architecture.md`](./data-architecture.md)  
  *Data ownership, flows, and lifecycle*

- [`technology-architecture.md`](./technology-architecture.md)  
  *Technology stack and reference architecture*

---

## 5. Decisions & Constraints

These documents preserve **architectural reasoning and trade-offs**.

- [`architecture-decisions.md`](./architecture-decisions.md)  
  *Architecture Decision Records (ADR)*

- [`architecture-constraints.md`](./architecture-constraints.md)  
  *Non-negotiable architectural rules and guardrails*

---

## 6. Operating & Governance Model

These documents define **who decides what** and **how decisions flow**.

- [`operating-model.md`](./operating-model.md)  
  *Roles, responsibilities, and authority*

- [`governance-model.md`](./governance-model.md)  
  *Decision workflows, approvals, and enforcement*

---

## 7. Compliance, Risk & Assurance

These documents describe **how compliance and risk are handled**.

- [`compliance-risk-model.md`](./compliance-risk-model.md)  
  *Regulatory mapping, risk assessment, and evidence preservation*

---

## 8. Observability & Intelligence

These documents explain **how runtime signals enrich architecture insight**.

- [`observability-intelligence.md`](./observability-intelligence.md)  
  *Telemetry, drift detection, and architecture intelligence*

---

## 9. Integration & Ecosystem

These documents define **how EAVIP interacts with the external world**.

- [`integration-ecosystem.md`](./integration-ecosystem.md)  
  *Integration patterns, event exchange, and external systems*

---

## 10. Roadmap & Evolution

These documents show **how the architecture evolves over time**.

- [`architecture-roadmap.md`](./architecture-roadmap.md)  
  *Phased evolution, priorities, and sequencing*

---

## Documentation Philosophy

All documents in this repository follow these rules:

- Decisions are always accompanied by reasoning
- Alternatives and trade-offs are explicitly stated
- Documents describe intent, not implementation detail
- Architecture truth is derived from a canonical model
- History is preserved; nothing is silently overwritten

---

## Final Note

This documentation set is intentionally structured to act as:
- A **learning reference** for enterprise architecture
- A **practical playbook** for real-world implementation
- A **living architectural memory** for EAVIP

When EAVIP is fully implemented, these documents will not only describe
the platform — they will demonstrate its value as a case study.
