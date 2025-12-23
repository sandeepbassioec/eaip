# Permissions, Access Control & Multi-Tenant Authorization Model

## Purpose

This document defines the **authorization model** for the Enterprise Architecture
Visibility & Intelligence Platform (EAVIP).

It ensures:
- **Least privilege** without blocking discovery
- **Clear ownership & accountability**
- **Safe cross-organization visibility**
- **Audit-ready decisions**
- **Scalability across SaaS and BYOC**

Authorization is **graph-aware**, **contextual**, and **time-aware**.

---

## Core Principles

1. **Visibility ≠ Mutability**
2. **Read is broad, write is narrow**
3. **Ownership drives authority**
4. **Decisions are explicit and auditable**
5. **Cross-org access is deliberate**
6. **Time-bound permissions are first-class**

---

## 1. Identity & Tenant Context

### 1.1 Tenant Hierarchy

Authorization evaluates context in this order:

Enterprise
└── Organization
└── Domain
└── Application
└── Component


Each request carries:
- TenantId
- OrganizationId
- UserId / ServiceId
- Roles
- EffectiveTime (for time-travel views)

---

## 2. Role Model (Enterprise-Grade)

### 2.1 Platform Roles (Global)

| Role | Capabilities |
|------|--------------|
| PlatformAdmin | Tenant setup, global policies |
| SecurityAdmin | Security & zero-trust policies |
| ComplianceAdmin | Regulations, audits, evidence |

---

### 2.2 Enterprise Roles

| Role | Capabilities |
|------|--------------|
| EnterpriseArchitect | Enterprise-wide modeling & governance |
| ExecutiveViewer | Read-only summaries & trends |

---

### 2.3 Organization Roles

| Role | Capabilities |
|------|--------------|
| OrgOwner | Ownership, approvals |
| OrgArchitect | Org-level architecture & decisions |
| OrgViewer | Read-only within org |

---

### 2.4 Application Roles

| Role | Capabilities |
|------|--------------|
| AppOwner | App ownership & approvals |
| AppArchitect | App modeling, ADRs |
| AppContributor | Propose changes |
| AppViewer | Read-only |

---

## 3. Permission Types (Atomic)

Permissions are **small and composable**.

### 3.1 Read Permissions
- View nodes
- View relationships
- View diagrams
- View history & time slices

### 3.2 Write Permissions
- Create / update nodes
- Create / update relationships
- Attach ADRs / requirements
- Propose changes

### 3.3 Approve Permissions
- Approve ADRs
- Approve cross-org dependencies
- Approve risk acceptance
- Approve exceptions

### 3.4 Govern Permissions
- Define policies
- Override with justification
- Close violations

---

## 4. Ownership & Authority

### 4.1 Ownership Rules

- Every node has **one owner**
- Ownership implies:
  - Edit authority
  - Approval responsibility
  - Accountability

Ownership is explicit and visible on the graph.

---

### 4.2 Delegation

Owners may:
- Delegate permissions
- Time-bound delegation
- Scope-limited delegation

All delegations are:
- Logged
- Auditable
- Revocable

---

## 5. Cross-Organization Access (CRITICAL)

### 5.1 Visibility by Default, Control by Policy

- **Read-only visibility** allowed across orgs
- **Write/approve** across orgs requires explicit grant

Use cases:
- Shared platforms
- Data producers/consumers
- M&A visibility

---

### 5.2 Cross-Org Contracts

Cross-org dependencies require:
- Contract node
- Approvers from both orgs
- Expiry / review date

Without contract:
- Dependency flagged
- Read-only visibility remains

---

## 6. Graph-Aware Authorization

### 6.1 Authorization as Graph Queries

Access decisions evaluate:
- Node ownership
- Relationship paths
- Role inheritance
- Time validity

Example:
- User can edit a component **only if**
  - Owns the application **or**
  - Is delegated by owner **and**
  - Time window is valid

---

## 7. Time-Aware Permissions

### 7.1 Temporal Access

Permissions can be:
- Permanent
- Time-boxed
- Future-effective

Supports:
- Audits
- Incident response
- Temporary programs

---

## 8. Change Proposal & Review Model

### 8.1 Propose vs Commit

Non-owners can:
- Propose changes
- Comment
- Attach evidence

Owners must:
- Review
- Approve or reject
- Record rationale

---

### 8.2 Review Trails

Every approval captures:
- Who approved
- When
- Why
- What changed

---

## 9. Diagram & View Permissions

- Views inherit graph permissions
- Sensitive overlays (security, compliance) are role-restricted
- Shareable read-only links are:
  - Time-bound
  - Scope-limited
  - Watermarked

---

## 10. Audit & Compliance Alignment

Authorization events generate:
- Immutable audit records
- Evidence for compliance
- Time-slice replay

Auditors can:
- View historical access
- Verify approvals
- Validate separation of duties

---

## 11. What This Model Avoids

- Global admins editing everything
- Hard-coded role logic
- Hidden ownership
- Untraceable approvals
- “Shadow architects”

---

## Outcome

With this model:
- Visibility scales safely
- Authority is clear
- Governance is enforceable
- Trust is earned and maintained

---

## Status

This document defines the **authoritative authorization model** for EAVIP.

All APIs, UIs, and integrations **must enforce these rules**.
