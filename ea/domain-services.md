# Domain Services, Policies & Cross-Aggregate Rules
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document explains **Domain Services**, **Domain Policies**, and
**cross-aggregate business rules** in a DDD-based system like EAVIP.

It answers the most confusing and commonly misused DDD questions:
- When logic does NOT belong inside an aggregate
- How to handle rules spanning multiple aggregates
- What a Domain Service really is (and what it is not)
- How policies differ from services
- How to keep aggregates small, pure, and maintainable

This document is meant to eliminate ambiguity permanently.

---

## Core Rule (Locked)

**If a business rule does not naturally belong to a single aggregate,
it does NOT go inside an aggregate.**

Forcing such logic into aggregates causes:
- Bloated aggregate roots
- Tight coupling
- Broken boundaries

---

## Why Domain Services Exist

Aggregates:
- Protect **local consistency**
- Enforce **invariants within a boundary**

But many real business rules:
- Span multiple aggregates
- Depend on external context
- Represent enterprise-level logic

Domain Services exist to handle exactly this.

---

## What a Domain Service IS

A Domain Service:
- Represents a **business operation**
- Has **no identity**
- Encapsulates **domain logic**
- Coordinates multiple aggregates
- Lives in the **domain layer**

It expresses **verbs**, not nouns.

---

## What a Domain Service IS NOT

A Domain Service is NOT:
- An application service
- A repository
- A command handler
- A utility/helper class
- An orchestration layer

If it mainly calls repositories or infrastructure APIs,
it is NOT a domain service.

---

## When to Create a Domain Service (Thumb Rules)

Create a Domain Service when:
1. A rule spans more than one aggregate
2. No single aggregate clearly owns the rule
3. The rule expresses business policy, not workflow
4. The rule must remain consistent across use cases

If a rule fits inside one aggregate → keep it there.

---

## Examples from EAVIP (Concrete)

### Example 1: Application Dependency Validation

Rule:
> An application cannot introduce a dependency that violates enterprise policies.

Why this is NOT inside `Application` aggregate:
- Policy is enterprise-wide
- Depends on other applications
- Depends on governance rules

Solution:
- `DependencyPolicyService`

---

### Example 2: Sunset Recommendation Logic

Rule:
> Recommend sunset when cost is high, value is low, and risk is acceptable.

Why NOT in `ApplicationPortfolio`:
- Requires metrics from multiple sources
- Depends on evolving scoring logic
- Used across reports and governance

Solution:
- `ModernizationPolicyService`

---

## Domain Policy vs Domain Service

### Domain Policy

A **policy**:
- Encodes a business rule
- Returns decisions or evaluations
- Has no side effects

Example:
- IsDependencyAllowed?
- IsApplicationCompliant?

Policies are often **pure functions**.

---

### Domain Service

A **service**:
- Uses policies
- Coordinates aggregates
- Enforces higher-level rules

Policies decide.  
Services apply.

---

## Structure Recommendation

### Domain Layer Structure

- Aggregates
- Value Objects
- Domain Services
- Domain Policies
- Domain Events

Infrastructure and application logic stay out.

---

## How Domain Services Are Used (Correct Flow)

1. CommandHandler receives request
2. Loads required aggregates
3. Invokes Domain Service
4. Domain Service applies rules
5. Aggregates are updated via methods
6. Aggregates raise domain events
7. Repository saves aggregates

Domain Services never persist data themselves.

---

## Cross-Aggregate Interaction Rules (Locked)

- Aggregates never call other aggregates
- Aggregates never load repositories
- Domain Services may reference multiple aggregates
- References across aggregates are by ID only

Violating this breaks aggregate isolation.

---

## Handling Transactions Across Aggregates

Rule:
**If multiple aggregates must change atomically, the design is wrong.**

Correct options:
- Eventual consistency
- Domain events
- Process managers (Sagas)

Do NOT use distributed transactions.

---

## Domain Services vs Application Services

| Aspect | Domain Service | Application Service |
|-----|---------------|--------------------|
| Layer | Domain | Application |
| Purpose | Business rules | Workflow orchestration |
| Knows infrastructure | No | Yes |
| Uses repositories | Indirect | Yes |
| Enforces invariants | Yes | No |

Confusing these two is the most common DDD mistake.

---

## Trade-offs

**Pros**
- Clean aggregates
- Clear ownership
- Reusable business logic
- Scales with complexity

**Cons**
- Requires deeper thinking
- More concepts to learn
- Easy to misuse initially

---

## Why This Approach Works Long-Term

- Prevents aggregate bloat
- Supports evolving business rules
- Aligns with enterprise-scale domains
- Makes refactoring safe

This is how large, long-lived systems stay sane.

---

## Final Mental Model

- Aggregates protect local consistency
- Domain Services enforce cross-boundary rules
- Policies express decisions
- Handlers orchestrate
- Infrastructure supports

If you respect these boundaries, DDD becomes simple.

---

## Next Step

Proceed to **Process Managers / Sagas & Eventual Consistency**  
File: `ea/process-managers-sagas.md`
