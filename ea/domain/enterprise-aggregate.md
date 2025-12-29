# Step 1 – Enterprise Aggregate (Domain-Only, Corrected)

---

## 1. Purpose

This document defines the **Enterprise Aggregate** for EAVIP.

It establishes:
- The **root of the entire domain model**
- The **highest business consistency boundary**
- The **starting point for all downstream architecture**

This aggregate is **pure domain**:
- No repositories
- No persistence
- No framework references
- No infrastructure concerns
- No multi-tenancy logic

---

## 2. Why Enterprise Is an Aggregate Root

### 2.1 Business Reasoning (WHY)

In EAVIP, **Enterprise** represents:

- The highest-level business boundary
- The legal, financial, and governance umbrella
- The owner of:
  - Organizations
  - Enterprise-wide applications
  - Architecture policies
  - Compliance posture
  - Decision accountability

From a TOGAF perspective:
- Enterprise = **Architecture Scope Boundary**
- Everything else exists *within* this scope

From a DDD perspective:
- Enterprise is the **root consistency boundary**
- All enterprise-wide invariants must be enforced here

Therefore:
> **Enterprise MUST be an Aggregate Root**

---

## 3. Aggregate Boundary Definition

### 3.1 Inside the Enterprise Aggregate

The Enterprise Aggregate owns:

- Enterprise identity
- Enterprise name and classification
- Lifecycle state
- Enterprise-level rules and invariants

It does **NOT** directly own:
- Organizations (separate aggregate)
- Applications (separate aggregate)
- Deployment models
- Metrics
- Decisions

It **references** them by identity only.

---

## 4. Invariants Enforced by Enterprise

### 4.1 Core Invariants

The Enterprise Aggregate enforces:

1. An Enterprise must always have:
   - A valid identifier
   - A non-empty name
2. An Enterprise lifecycle is explicit and controlled
3. An Enterprise cannot be deleted once activated
4. Enterprise identity is immutable

These are **business truths**, not technical constraints.

---

## 5. Domain Model (Conceptual)
Enterprise (Aggregate Root)
├── EnterpriseId (Value Object)
├── EnterpriseName (Value Object)
├── EnterpriseType (Value Object)
├── EnterpriseStatus (Value Object)
├── CreatedAt (Value Object)
└── Domain Events

---

## 6. Aggregate Root Definition (Conceptual Code)

> NOTE: This is **domain-only pseudocode** for understanding.
> It intentionally avoids frameworks, annotations, and persistence.

```csharp
public sealed class Enterprise
{
    private readonly List<IDomainEvent> _domainEvents = new();

    public EnterpriseId Id { get; }
    public EnterpriseName Name { get; private set; }
    public EnterpriseType Type { get; }
    public EnterpriseStatus Status { get; private set; }
    public Instant CreatedAt { get; }

    private Enterprise(
        EnterpriseId id,
        EnterpriseName name,
        EnterpriseType type,
        EnterpriseStatus status,
        Instant createdAt)
    {
        Id = id;
        Name = name;
        Type = type;
        Status = status;
        CreatedAt = createdAt;
    }

    public static Enterprise Create(
        EnterpriseId id,
        EnterpriseName name,
        EnterpriseType type,
        Instant createdAt)
    {
        var enterprise = new Enterprise(
            id,
            name,
            type,
            EnterpriseStatus.Draft,
            createdAt);

        enterprise.Raise(new EnterpriseCreated(id));

        return enterprise;
    }

    public void Activate()
    {
        if (Status == EnterpriseStatus.Active)
            return;

        Status = EnterpriseStatus.Active;
        Raise(new EnterpriseActivated(Id));
    }

    private void Raise(IDomainEvent domainEvent)
    {
        _domainEvents.Add(domainEvent);
    }

    public IReadOnlyCollection<IDomainEvent> DomainEvents => _domainEvents.AsReadOnly();
}
```


