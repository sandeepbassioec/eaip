# Commercial Model, Licensing & Tenant Isolation Strategy
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines the **commercial model, licensing strategy, and tenant isolation**
for EAVIP across SaaS, BYOC, and On-Prem deployments.

It explains:
- How value is monetized without penalizing adoption
- How licensing aligns with enterprise buying behavior
- How tenant isolation is enforced technically and contractually
- Why licensing choices reinforce architectural principles
- Trade-offs between simplicity, fairness, and scalability

This document serves as a **reference monetization architecture**.

---

## Core Principle (Locked)

**Licensing must reflect value delivered, not technical implementation details.**

Customers should pay for **outcomes and scale**, not for internal mechanics.

---

## Target Buyer Personas

Primary buyers:
- CIO / CTO
- Enterprise Architecture Head
- CISO (for security-focused expansions)
- Procurement (commercial validation)

Secondary influencers:
- Enterprise Architects
- Platform Engineering
- Governance & Compliance

Licensing must satisfy **both strategic buyers and operational users**.

---

## Commercial Deployment Models

EAVIP commercial offerings align with deployment models:

1. SaaS (Subscription-based)
2. BYOC (Subscription + Infrastructure-owned)
3. On-Prem (License + Maintenance)

Each has different cost drivers and pricing levers.

---

## SaaS Commercial Model

### Pricing Dimensions

SaaS pricing is based on:
- Number of organizations modeled
- Number of applications tracked
- Enabled capability tier
- Data retention period
- Advanced intelligence add-ons (later phases)

### Why This Works

- Aligns cost with enterprise scale
- Predictable budgeting
- Encourages portfolio completeness
- Avoids per-user friction

Users are not penalized for collaboration.

---

## BYOC Commercial Model

### Pricing Dimensions

- Base platform subscription
- Scale-based pricing (applications / orgs)
- Optional managed operations
- Optional advanced intelligence modules

### Rationale

- Customer already pays for cloud infra
- Vendor charges for platform value, not infrastructure
- Clear separation of responsibilities

This model reduces vendor lock-in fear.

---

## On-Prem Commercial Model

### Pricing Dimensions

- Per-deployment license
- Maximum supported scale tier
- Annual maintenance & support
- Optional professional services

### Rationale

- Aligns with traditional enterprise procurement
- Supports regulated industries
- Predictable long-term cost

On-Prem customers trade flexibility for control.

---

## Capability-Based Licensing (Critical)

Licensing is tiered by **capability sets**, not features.

### Example Tiers

- Foundation (Portfolio, Modeling, Diagrams)
- Enablement (Decisions, Editing, Import/Export)
- Intelligence (Metrics, Drift, Simulation, Scoring)

This ensures:
- Clear value progression
- No artificial feature fragmentation
- Natural upsell paths

---

## Tenant Isolation Strategy

### SaaS Isolation

- Logical tenant isolation
- Strong authorization boundaries
- Tenant-scoped encryption keys
- Data access enforced at every layer

### BYOC Isolation

- Physical isolation by account/project
- Customer-controlled networking
- Vendor access via explicit roles

### On-Prem Isolation

- Single-tenant by deployment
- Customer-controlled access
- No external data sharing

Isolation is enforced **architecturally**, not contractually alone.

---

## Data Ownership & Rights

Rules:
- Customer owns all architecture data
- Vendor has no reuse rights without consent
- Metadata may be used only for anonymized improvement (opt-in)
- Export is always supported

Architecture visibility must never become vendor leverage.

---

## License Enforcement Mechanisms

Licensing is enforced via:
- Platform Configuration Aggregate
- Capability flags
- Usage metering (non-invasive)
- Governance-level checks

No hard kill-switches.
No sudden shutdowns.

---

## Overuse & Fair-Use Handling

If limits are exceeded:
- Warnings are issued
- Grace periods apply
- Expansion paths are suggested
- Human discussion is encouraged

Licensing disputes should never disrupt operations.

---

## Trial & Adoption Strategy

- Time-limited trials
- Scope-limited pilots
- Read-only exploration modes
- Progressive capability unlocks

This lowers adoption friction.

---

## Trade-offs

**Pros**
- Fair and scalable pricing
- Aligns with enterprise buying behavior
- Reduces user resistance
- Supports long-term relationships

**Cons**
- More complex than per-user pricing
- Requires clear communication
- Needs accurate usage measurement

---

## Why This Model Works

- Matches enterprise value perception
- Encourages full architecture modeling
- Avoids penalizing collaboration
- Preserves customer trust

Commercial strategy reinforces architectural intent.

---

## Final Mental Model

- License value, not mechanics
- Scale with architecture, not users
- Isolate tenants by design
- Monetize intelligence, not access

---

## Next Step

Proceed to **Change Management, Upgrades & Continuous Evolution**  
File: `ea/change-management.md`
