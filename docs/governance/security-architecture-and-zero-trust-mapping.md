# Security Architecture & Zero-Trust Mapping on the Enterprise Graph

## Purpose

This document defines how **security architecture** is modeled, visualized, and
continuously validated within the **Enterprise Graph**.

It enables enterprises to:
- See **trust boundaries** across orgs, apps, components, cloud, and externals
- Understand **who can talk to whom, how, and why**
- Map **zero-trust principles** directly onto architecture reality
- Detect **security drift** early and explain it with evidence

Security is not a checklist — it is **architecture you can see and reason about**.

---

## Core Principles

1. **Zero Trust by Design**
2. **Trust Boundaries are First-Class**
3. **Identity is the new perimeter**
4. **Data sensitivity drives controls**
5. **Observed reality is continuously validated**
6. **Every control is explainable**

---

## 1. Security as a Graph (Foundational)

### 1.1 Security is Modeled, Not Assumed

Security concepts are modeled as **nodes and relationships** in the graph.

**Security Nodes**
- IdentityProvider
- Principal (User / Service)
- Credential
- Policy
- Control
- TrustBoundary
- DataClassification

**Security Relationships**
- AUTHENTICATES
- AUTHORIZES
- TRUSTS
- SECURED_BY
- ENCRYPTED_WITH
- VIOLATES

This allows **end-to-end traceability** from identity → component → data.

---

## 2. Trust Boundary Modeling (CRITICAL)

### 2.1 Trust Boundary Definition

A **TrustBoundary** node defines a change in security posture.

Examples:
- Organization boundary
- Network boundary
- Cloud account / subscription
- Kubernetes namespace
- External partner boundary

---

### 2.2 Boundary Crossing Relationships

Whenever a relationship crosses a trust boundary, it must declare:
- Authentication method
- Authorization mechanism
- Encryption in transit
- Contract / approval

**If not declared → violation**

---

## 3. Identity & Authentication Mapping

### 3.1 Identity Sources

Modeled as nodes:
- Enterprise IdP
- Cloud IAM
- External IdP
- Service Identity Provider

---

### 3.2 Authentication Flows

Authentication is modeled as **flows**, not assumptions.

Examples:
- User → IdP → Application
- Service → Token Service → API
- External Partner → Gateway → Internal Service

Each flow records:
- Protocol (OIDC, SAML, mTLS)
- Token scope
- Lifetime
- Trust level

---

## 4. Authorization & Access Control

### 4.1 Authorization as Relationships

Authorization is modeled as:
- Principal → AUTHORIZES → Resource
- Policy → ENFORCES → Action

Supports:
- RBAC
- ABAC
- Policy-based access

---

### 4.2 Least Privilege Validation

The graph validates:
- Excessive permissions
- Orphaned access
- Privilege creep over time

Drift is detected when:
- Observed access > Intended access

---

## 5. Data Security & Sensitivity Mapping

### 5.1 Data Classification

Each **DataEntity / Dataset** node has:
- Sensitivity (Public / Internal / Confidential / Regulated)
- Residency requirements
- Retention requirements

---

### 5.2 Data Flow Controls

Every data flow must declare:
- Encryption in transit
- Encryption at rest
- Masking / tokenization (if applicable)

Violations appear **directly on data-flow diagrams**.

---

## 6. Cloud Security Modeling

### 6.1 Cloud Security Nodes

Modeled entities:
- CloudAccount / Subscription
- Network (VPC / VNet)
- SecurityGroup / Firewall
- ManagedIdentity
- KeyManagementService

---

### 6.2 Cloud Security Relationships

Examples:
- DEPLOYED_IN (Region)
- PROTECTED_BY (SecurityGroup)
- AUTHENTICATES_WITH (IAM)
- ENCRYPTED_WITH (KMS)

Supports:
- Multi-cloud
- BYOC
- Hybrid

---

## 7. External & Third-Party Security

### 7.1 External Dependency Security

External systems are modeled explicitly:
- ExternalApplication
- ExternalService
- Vendor

Captured attributes:
- Trust level
- Data exposure
- SLA / contract reference
- Security certification (if any)

---

### 7.2 Risk Surfacing

The platform highlights:
- Sensitive data flowing to external systems
- External calls bypassing gateways
- Shadow integrations

---

## 8. Zero-Trust Validation Engine

### 8.1 Zero-Trust Assertions

Examples:
- No implicit trust across boundaries
- Every call must be authenticated
- Authorization must be explicit
- Data encryption is mandatory

These are **policies over the graph**, not code checks.

---

### 8.2 Violations & Explainability

For every violation, the system answers:
- What boundary was crossed?
- What control was missing?
- Which data was exposed?
- When did it start?
- What is the impact?

---

## 9. Security Views & Diagrams (Auto-Generated)

### 9.1 Security Overlay Mode

Any architecture diagram can toggle:
- Trust boundaries
- Auth flows
- Data sensitivity
- Control coverage

---

### 9.2 Security-Focused Diagrams

Auto-generated:
- Trust Boundary Diagram
- AuthN/AuthZ Flow Diagram
- Data Protection Diagram
- Cloud Security Posture Diagram

All derived from the same graph.

---

## 10. Security Over Time (VERY IMPORTANT)

Security is **time-aware**:
- When was a boundary added?
- When did a control disappear?
- How long has this violation existed?

Supports:
- Incident forensics
- Audit reviews
- Continuous improvement

---

## What This Model Avoids

- Spreadsheet security reviews
- Static threat models
- Tool-specific silos
- Invisible trust assumptions
- Security theater

---

## Outcome

With this model:
- Zero Trust becomes **visible**
- Security is **architectural**, not aspirational
- Drift is detected **before incidents**
- Audits become **graph queries**, not fire drills

---

## Status

This document defines the **authoritative security and zero-trust model** for EAVIP.

All security features, validations, and diagrams **must derive from this graph**.
