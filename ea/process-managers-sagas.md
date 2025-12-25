# Process Managers (Sagas) & Eventual Consistency
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document explains **Process Managers (also known as Sagas)** and
**Eventual Consistency** in a DDD + CQRS system like EAVIP.

It answers the hardest practical questions:
- When a single transaction is not possible, what do we do?
- How do multiple aggregates coordinate safely?
- What is a Saga really (beyond theory)?
- Orchestration vs Choreography — when to use which?
- How failures, retries, and compensations are handled

This document is execution-grade and meant as a **permanent reference**.

---

## Core Rule (Locked)

**Aggregates must never coordinate directly with other aggregates.**

If business flow requires multiple aggregates to change:
- Do NOT use distributed transactions
- Do NOT load multiple aggregates inside one aggregate
- Use a Process Manager (Saga)

---

## Why Process Managers Exist

In real systems:
- Business processes span time
- Steps may fail
- Human approval may be required
- Systems are distributed

Strong consistency across all steps is:
- Expensive
- Fragile
- Often impossible

Therefore we embrace **Eventual Consistency**.

---

## What Is a Process Manager (Saga)?

A Process Manager is:
- A long-running business process
- Driven by **domain events**
- Responsible for **coordination, not business rules**
- Stateful (tracks progress)
- Explicit about success and failure

A Process Manager:
- Listens to events
- Sends commands
- Tracks state
- Handles retries and compensation

---

## What a Process Manager IS NOT

A Process Manager is NOT:
- An aggregate
- A domain service
- A command handler
- A workflow engine UI
- A distributed transaction

It does not enforce business invariants.
Aggregates still own their own rules.

---

## When You Need a Saga (Thumb Rules)

Use a Process Manager when:
1. More than one aggregate must change
2. Changes cannot be atomic
3. Steps may fail independently
4. Time gaps exist between steps
5. Human or external system involvement exists

If all changes fit in one aggregate → no saga needed.

---

## Example from EAVIP (Concrete)

### Scenario: Application Sunset Process

Steps:
1. Application marked as "Candidate for Sunset"
2. Dependencies validated
3. Governance approval requested
4. Dependent applications notified
5. Final sunset decision recorded

This process:
- Spans multiple aggregates
- Involves approval
- Cannot be transactional

**Solution:** `ApplicationSunsetProcessManager`

---

## Process Manager Responsibilities (Strict)

A Process Manager:
- Subscribes to domain events
- Decides the next step
- Issues commands to aggregates
- Maintains its own state
- Handles retries and compensation

A Process Manager never:
- Modifies aggregates directly
- Applies business rules internally
- Bypasses governance

---

## Orchestration vs Choreography

### Orchestration (Chosen Default)

- Central coordinator (Process Manager)
- Explicit flow
- Easier reasoning and debugging

**Used in EAVIP because:**
- Governance-heavy flows
- Approval workflows
- High audit requirements

---

### Choreography

- Each component reacts to events
- No central controller

**Why Not Default**
- Harder to trace
- Difficult to audit
- Easy to create hidden coupling

Choreography is allowed only for simple, low-risk flows.

---

## State Management in Process Managers

A Process Manager tracks:
- Current step
- Completed steps
- Pending actions
- Failure reasons
- Retry counts

State is:
- Persisted
- Versioned
- Auditable

---

## Failure Handling & Compensation

### Failure Types
- Temporary failure (retry)
- Permanent failure (compensate)
- External system unavailable
- Human rejection

### Compensation
- Explicit compensating commands
- No magical rollback
- Business-defined recovery

Example:
- Revert application status
- Cancel pending approvals
- Notify stakeholders

---

## Eventual Consistency Explained (Clearly)

Eventual consistency means:
- System is not immediately consistent
- But will become consistent over time
- With well-defined transitions

This is acceptable when:
- Business tolerates short delays
- Processes are explicit
- Users are informed of state

EAVIP makes consistency **visible**, not hidden.

---

## How Process Managers Fit with CQRS

- Commands trigger aggregate changes
- Aggregates emit events
- Process Managers react to events
- Process Managers send new commands

No circular dependencies.
No shared state.

---

## Persistence Rules (Locked)

- One Process Manager instance per business process
- Identified by a correlation ID
- Events correlated explicitly
- No in-memory-only sagas

---

## Anti-Patterns (Avoid at All Costs)

- Putting saga logic inside aggregates
- Using sagas for single-aggregate updates
- Hiding failure states
- Using distributed transactions
- Infinite retries without visibility

These lead to:
- Unpredictable systems
- Data corruption
- Operational nightmares

---

## Trade-offs

**Pros**
- Scales across services
- Handles real-world failures
- Clear audit trails
- Supports human workflows

**Cons**
- More moving parts
- More state to manage
- Requires careful design

---

## Why This Works in Enterprises

- Matches real business processes
- Aligns with governance needs
- Survives partial failures
- Enables long-running workflows

This is how **enterprise systems actually work**.

---

## Final Mental Model

- Aggregates enforce local rules
- Domain Services enforce cross-aggregate rules
- Process Managers coordinate time-based flows
- Events drive progression
- Eventual consistency is intentional

Once this clicks, distributed systems stop being scary.

---

## Next Step

Proceed to **API Design & Contract Strategy (OpenAPI, Versioning, Evolution)**  
File: `ea/api-design-contracts.md`
