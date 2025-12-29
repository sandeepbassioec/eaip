# Step 2 – Organization Aggregate (Domain-Only, Corrected)

---

## 1. Purpose

This document defines the **Organization Aggregate** in EAVIP.

The Organization aggregate represents:
- A **business-operating unit** inside an Enterprise
- A **delegated governance boundary**
- The **owner of application portfolios and teams**

This aggregate is **pure domain**:
- No persistence logic
- No repositories
- No infrastructure
- No tenant logic
- No application wiring

---

## 2. Why Organization Is a Separate Aggregate Root

### 2.1 Business Reasoning (WHY)

In real enterprises:

- One Enterprise can have **many organizations**
  - Business units
  - Subsidiaries
  - Departments
  - Regions
- Each organization:
  - Owns applications
  - Has partial autonomy
  - Has its own lifecycle
  - May evolve independently

From **TOGAF**:
- Organization aligns with **Business Architecture decomposition**
- It is a **manageable scope** for architecture ownership

From **DDD**:
- Organization has its **own consistency rules**
- Organization changes should not require Enterprise-level transactions

Therefore:
> **Organization must be its own Aggregate Root**

---

## 3. Aggregate Boundary Definition

### 3.1 Inside the Organization Aggregate

The Organization aggregate owns:

- Organization identity
- Organization name
- Organization type (Business Unit, Subsidiary, Region, etc.)
- Lifecycle status
- Reference to its Enterprise

### 3.2 Outside the Aggregate

Organization does **NOT** own:

- Applications
- Components
- Deployments
- Metrics
- Compliance records

Those are **separate aggregates** that *belong to* an Organization.

---

## 4. Relationship with Enterprise

### Decision

Organization **references** Enterprise by **EnterpriseId only**.

### WHY

- Prevents cross-aggregate object graphs
- Avoids distributed transactions
- Preserves aggregate independence
- Enables scalable evolution

Correct:
Organization -> Enterprise object

---

## 5. Invariants Enforced by Organization

The Organization aggregate enforces:

1. Organization must belong to exactly **one Enterprise**
2. Organization name must be unique **within an Enterprise**
3. Organization lifecycle must be explicit
4. Organization cannot be activated if Enterprise is inactive
5. Organization identity is immutable

These are **business rules**, not database constraints.

---

## 6. Domain Model (Conceptual)
Organization (Aggregate Root)
├── OrganizationId (Value Object)
├── EnterpriseId (Value Object)
├── OrganizationName (Value Object)
├── OrganizationType (Value Object)
├── OrganizationStatus (Value Object)
├── CreatedAt (Value Object)
└── Domain Events


---

## 7. Aggregate Root Definition (Conceptual Code)

> Domain-only pseudocode  
> No frameworks, no persistence

```csharp
public sealed class Organization
{
    private readonly List<IDomainEvent> _domainEvents = new();

    public OrganizationId Id { get; }
    public EnterpriseId EnterpriseId { get; }
    public OrganizationName Name { get; private set; }
    public OrganizationType Type { get; }
    public OrganizationStatus Status { get; private set; }
    public Instant CreatedAt { get; }

    private Organization(
        OrganizationId id,
        EnterpriseId enterpriseId,
        OrganizationName name,
        OrganizationType type,
        OrganizationStatus status,
        Instant createdAt)
    {
        Id = id;
        EnterpriseId = enterpriseId;
        Name = name;
        Type = type;
        Status = status;
        CreatedAt = createdAt;
    }

    public static Organization Create(
        OrganizationId id,
        EnterpriseId enterpriseId,
        OrganizationName name,
        OrganizationType type,
        Instant createdAt)
    {
        var organization = new Organization(
            id,
            enterpriseId,
            name,
            type,
            OrganizationStatus.Draft,
            createdAt);

        organization.Raise(new OrganizationCreated(id, enterpriseId));
        return organization;
    }

    public void Activate()
    {
        if (Status == OrganizationStatus.Active)
            return;

        Status = OrganizationStatus.Active;
        Raise(new OrganizationActivated(Id));
    }

    private void Raise(IDomainEvent domainEvent)
    {
        _domainEvents.Add(domainEvent);
    }

    public IReadOnlyCollection<IDomainEvent> DomainEvents => _domainEvents.AsReadOnly();
}
```

