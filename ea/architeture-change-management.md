# Architecture Change Management, Upgrades & Continuous Evolution
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **TOGAF Phase H – Architecture Change Management** for EAVIP.

It explains:
- How architectural change is proposed, assessed, approved, and executed
- How upgrades are handled across SaaS, BYOC, and On-Prem models
- How drift, learning, and outcomes feed back into earlier TOGAF phases
- Why continuous evolution is governed, not ad-hoc

This is the **operational playbook** for keeping architecture alive over time.

---

## Core Principle (Locked)

**Architecture change is inevitable; unmanaged change is unacceptable.**

Change must be:
- Visible
- Explainable
- Governed
- Reversible where possible

---

## Types of Architectural Change

EAVIP classifies change into clear categories to avoid ambiguity:

1. **Corrective Change**
   - Fixes defects or drift
   - Example: unauthorized dependency detected

2. **Adaptive Change**
   - Responds to environment or regulation
   - Example: new compliance requirement

3. **Evolutionary Change**
   - Improves capability or structure
   - Example: re-architecture for scalability

4. **Transformational Change**
   - Strategic shift
   - Example: cloud migration, app sunset

Each type follows a different governance intensity.

---

## Change Triggers

Architecture change can be triggered by:
- Observability & drift detection
- New business goals
- Risk or compliance findings
- Technology obsolescence
- Cost or value signals
- Human proposals

Triggers are first-class inputs, not informal requests.

---

## Change Proposal Lifecycle

### Step 1: Proposal Creation
- Change intent captured
- Scope defined
- Affected entities identified
- Rationale documented (WHY mandatory)

### Step 2: Impact Analysis
- Dependency blast radius
- Security implications
- Compliance impact
- Cost & value effects

### Step 3: Options & Trade-offs
- Multiple approaches evaluated
- Pros / cons documented
- Risks acknowledged

### Step 4: Approval
- Role-based approval
- Conditional or time-bound approvals supported
- Rejection is recorded with rationale

### Step 5: Execution & Tracking
- Change linked to delivery artifacts
- Progress tracked
- Deviations monitored

### Step 6: Outcome Review
- Expected vs actual outcomes compared
- Decision regret tracked
- Learnings fed back into governance

---

## Architecture Change Governance

### Governance Intensity Matrix

| Change Type | Automation | Human Approval | Audit |
|---|---|---|---|
| Corrective | High | Optional | Yes |
| Adaptive | Medium | Required | Yes |
| Evolutionary | Low | Required | Yes |
| Transformational | Minimal | Mandatory | Extensive |

Governance scales with risk.

---

## Upgrade Strategy (Platform-Level)

### SaaS
- Rolling upgrades
- Backward-compatible APIs
- Feature flags
- No forced customer downtime

### BYOC
- Customer-approved upgrade windows
- Version pinning
- Pre-upgrade validation

### On-Prem
- Explicit upgrade packages
- Compatibility checks
- Rollback paths required

All upgrades are **architectural changes**, not just ops tasks.

---

## Backward Compatibility & Deprecation

Rules:
- Deprecation is announced, not silent
- Sunset timelines are explicit
- Migration guidance is mandatory
- Old versions remain supported for a defined period

Customers are never surprised.

---

## Drift as Input to Change

Detected drift:
- Does NOT auto-enforce changes
- Triggers evaluation
- May result in:
  - Exception approval
  - Architecture update
  - Enforcement action

Drift becomes a **learning signal**, not a failure.

---

## Feedback Loop into TOGAF ADM

Phase H feeds back into:
- Phase A (Vision) when goals change
- Phase B (Business) when capabilities evolve
- Phase C (Application/Data) when structure changes
- Phase D (Technology) when platforms shift

ADM remains **circular and alive**.

---

## Documentation & Traceability (Locked)

Every change must link to:
- Goals
- Constraints
- Assumptions
- Trade-offs
- Outcomes

Changes without reasoning are non-compliant.

---

## Metrics for Change Effectiveness

- Time to approve change
- Time to execute change
- Number of unplanned changes
- Reduction in drift over time
- Decision regret score

These metrics improve governance maturity.

---

## Trade-offs

**Pros**
- Predictable evolution
- Reduced risk
- Organizational learning
- Strong audit posture

**Cons**
- Requires discipline
- Initial overhead
- Cultural adjustment

---

## Why This Model Works

- Accepts reality of change
- Prevents architectural decay
- Aligns with enterprise governance
- Enables long-term agility

Architecture becomes a **managed asset**, not static documentation.

---

## Final Mental Model

- Change is constant
- Visibility enables control
- Governance enables trust
- Learning enables evolution

---

## Next Step

Proceed to **Final TOGAF Cycle Closure & Operating Model**  
File: `ea/togaf-cycle-closure.md`
