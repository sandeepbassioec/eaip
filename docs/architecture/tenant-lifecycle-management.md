# Tenant Lifecycle Management

## Purpose

This document defines the authoritative tenant lifecycle management model
for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It ensures that:
- Tenant creation, evolution, and exit are predictable
- Data integrity and isolation are preserved at every stage
- Commercial, operational, and governance concerns remain aligned
- SaaS, BYOC, and On-Prem deployments follow the same lifecycle logic

This is the tenant lifecycle contract for EAVIP.

---

## Core Principles (Locked)

1. Tenant isolation is absolute at every lifecycle stage  
2. Lifecycle transitions are explicit and auditable  
3. No tenant action is silent or implicit  
4. Data ownership and responsibility are always clear  
5. Exit is as intentional as onboarding  
6. Commercial state aligns with technical state  

---

## Tenant Lifecycle Stages

Every tenant progresses through the following lifecycle stages:

- Provisioned  
- Active (Pilot or Production)  
- Suspended  
- Offboarded  
- Archived  

Transitions between stages are governed and recorded.

---

## Stage 1: Tenant Provisioning

### Description

Initial creation of a tenant environment.

### Activities

- Tenant identifier generation
- Deployment model selection (SaaS, BYOC, On-Prem)
- Initial license assignment
- Default governance configuration
- Security baseline application

### Rules

- Tenant isolation enforced from first operation
- No access before provisioning completes
- Provisioning is fully auditable

---

## Stage 2: Active – Pilot

### Description

Tenant operates under pilot or trial conditions.

### Activities

- Architecture modeling enabled
- Governance workflows active
- Pilot license enforced
- Feedback capture enabled

### Rules

- Pilot scope aligned with Phase-1 capabilities
- Pilot expiration date defined
- No production guarantees implied

---

## Stage 3: Active – Production

### Description

Tenant is fully operational under a commercial agreement.

### Activities

- Production license enforcement
- Full operational monitoring
- Backup and recovery enabled
- Support model activated

### Rules

- License compliance continuously enforced
- Operational SLAs apply
- Governance and audit fully active

---

## Stage 4: Tenant Suspension

### Description

Temporary restriction of tenant activity.

### Triggers

- License expiration
- Contractual issues
- Policy violations
- Administrative action

### Behavior

- Read-only access by default
- No data mutation allowed
- Governance workflows paused
- Data retained according to policy

Suspension is reversible.

---

## Stage 5: Tenant Offboarding

### Description

Controlled termination of tenant usage.

### Activities

- Formal offboarding request
- Data export (where contractually required)
- License deactivation
- Access revocation

### Rules

- Offboarding is deliberate and documented
- Data handling follows retention policy
- No immediate data destruction

---

## Stage 6: Archival

### Description

Long-term retention of tenant data after offboarding.

### Activities

- Data archived according to policy
- Access restricted to authorized roles
- Audit evidence preserved

### Rules

- Archived data is immutable
- Retrieval requires explicit authorization
- Archival duration is policy-driven

---

## Data Handling Across Lifecycle

- Tenant data never crosses tenant boundaries
- Lifecycle stage affects mutability, not ownership
- Deletion is governed and audited
- Derived data rebuilt or purged as appropriate

---

## License & Commercial Alignment

- Lifecycle stage must reflect license state
- License expiry triggers suspension, not deletion
- Commercial upgrades do not require reprovisioning
- Downgrades affect capability access, not data

---

## On-Prem Specific Considerations

- Customer controls infrastructure lifecycle
- Platform governs logical tenant lifecycle
- Clear responsibility
