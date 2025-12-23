# SaaS Subscription, Metering & Pricing (Technical)

## Purpose

This document defines the **technical model** for:
- Subscriptions and plans
- Feature entitlements
- Usage metering
- Quotas and limits
- Billing signals (without pricing numbers)

It ensures that **commercial rules are enforced by architecture**, not by UI or policy.

---

## Core Principles

1. Entitlements are enforced server-side
2. Usage is metered objectively
3. Limits degrade gracefully
4. Same model works for SaaS and BYOC
5. Billing systems are consumers, not authorities

---

## 1. Subscription Model

### Subscription Scope
- Subscriptions are **workspace-scoped**
- One workspace = one active subscription
- Subscription changes are versioned

### Subscription Entity
- SubscriptionId
- WorkspaceId
- PlanId
- Status (Trial / Active / Suspended / Expired)
- StartDate
- EndDate
- Version

---

## 2. Plan Definition (Technical View)

Plans define **capabilities and limits**, not UI behavior.

### Plan Attributes
- PlanId
- PlanType (Free / Team / Enterprise / BYOC)
- FeatureFlags
- Quotas
- HardLimits
- SoftLimits

### Examples
- MaxApplications
- MaxUsers
- MaxIntegrations
- EventDeliveryLimit
- DiagramCount
- AuditRetentionDays

---

## 3. Feature Entitlements

### Feature Model
- FeatureKey
- Enabled (true/false)
- Constraints (optional)

### Enforcement Rules
- Checked in application layer
- Never trusted from client
- Evaluated per request

### Examples
- ADR approvals enabled
- Advanced diagrams enabled
- External webhooks enabled
- BYOC deployment enabled

---

## 4. Usage Metering

### Metered Dimensions

| Dimension | Description |
|---------|-------------|
| Applications | Count of registered apps |
| Users | Active users |
| ADRs | Created / approved |
| Diagrams | Stored versions |
| Events | Published / delivered |
| Webhooks | Delivery attempts |
| Storage | Artifact size |
| API Calls | Requests per period |

---

### Metering Rules
- Usage is recorded **after successful operation**
- Failed attempts do not count
- Metering is tenant-scoped
- Metering is immutable

---

## 5. Quotas & Limits

### Hard Limits
- Operation is blocked
- Clear error returned
- Audit event recorded

### Soft Limits
- Warning emitted
- Grace period allowed
- Event sent to admins

### Degradation Strategy
- Read-only mode
- Disable non-critical features
- Preserve core access

---

## 6. Enforcement Points

### Enforced At
- API Gateway (coarse)
- Application Services (strict)
- Event Exchange (delivery caps)

### Forbidden
- UI-only enforcement
- Client-side checks
- Manual overrides without audit

---

## 7. Billing Signal Generation

### Billing Events (Outbound)

Examples:
- Usage.Recorded
- Quota.Exceeded
- Subscription.Changed
- Trial.Expired

### Characteristics
- Immutable
- Workspace-scoped
- Versioned
- Delivered via Event Exchange

> Billing systems **consume** these events  
> They do not calculate usage themselves

---

## 8. SaaS vs BYOC Behavior

### SaaS
- Full metering enabled
- All limits enforced
- Central billing

### BYOC
- Metering optional
- Feature entitlements enforced
- Billing handled externally or contractually

---

## 9. Trial Management

### Trial Characteristics
- Time-bound
- Limited quotas
- Full feature visibility (optional)

### Trial End Behavior
- Read-only access
- Export allowed
- No destructive actions

---

## 10. Auditing & Transparency

- All usage recorded
- Admins can view usage dashboards
- Disputes traceable via audit logs

---

## 11. Security Considerations

- Metering data is tamper-proof
- No client-submitted usage data
- Usage records are append-only

---

## Forbidden Anti-Patterns

❌ Usage calculated in UI  
❌ Billing system calling internal DBs  
❌ Silent throttling  
❌ Unexplained feature disablement  
❌ Manual quota changes without audit  

---

## Outcome

With this model:
- Pricing scales with value
- Abuse is controlled
- Enterprise contracts are enforceable
- SaaS and BYOC share the same core

---

## Status

This document defines the **authoritative technical subscription and metering model**.

Any change to entitlements, limits, or billing signals **must update this file**.
