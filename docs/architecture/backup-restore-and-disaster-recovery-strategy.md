# Backup, Restore & Disaster Recovery Strategy

## Purpose

This document defines the authoritative backup, restore, and disaster recovery
strategy for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It ensures that:
- Architecture data is never lost silently
- Recovery procedures are predictable and rehearsed
- SaaS, BYOC, and On-Prem deployments share the same recovery logic
- Data integrity is prioritized over speed

This is the resilience and continuity contract for EAVIP.

---

## Core Principles (Locked)

1. Data integrity overrides recovery speed  
2. Backups are useless unless restores are tested  
3. Recovery must be deterministic and documented  
4. Tenant isolation applies during recovery  
5. Automation is preferred; manual paths must exist  
6. Disaster recovery is a business capability, not just a technical one  

---

## Data Classification for Recovery

EAVIP data is classified for recovery purposes into:

- Enterprise Graph data
- Governance and audit data
- Document metadata and content
- Search and index data
- Configuration and secrets (references only)

Each category has distinct recovery characteristics.

---

## Backup Strategy

### Enterprise Graph (Neo4j)

- Full backups scheduled regularly
- Incremental backups between full snapshots
- Backups are immutable and encrypted
- Backup integrity verified automatically

---

### Relational Data (PostgreSQL)

- Logical backups for portability
- Point-in-time recovery enabled where supported
- Backups encrypted and access-controlled

---

### Search Indexes (OpenSearch)

- Index snapshots taken regularly
- Index data treated as rebuildable
- Snapshots used for faster recovery only

---

### Documents & Attachments

- Stored in durable object storage or equivalent
- Versioned and immutable once approved
- Backup aligned with metadata backups

---

## Restore Procedures

### Standard Restore

Used for:
- Accidental deletion
- Data corruption
- Limited-scope failures

Steps:
- Identify recovery point
- Restore affected data stores
- Rebuild derived indexes
- Validate integrity and consistency

---

### Full Platform Restore

Used for:
- Catastrophic failure
- Environment rebuild
- Disaster recovery drills

Steps:
- Provision clean environment
- Restore core data stores
- Rehydrate indexes and projections
- Validate tenant isolation
- Resume controlled access

---

## Disaster Recovery Scenarios

Disaster scenarios include:
- Region or data center loss
- Irrecoverable infrastructure failure
- Widespread data corruption
- Security incident requiring rebuild

Each scenario has a documented recovery path.

---

## Recovery Objectives

Recovery objectives are defined at platform level:

- Recovery Point Objective (RPO): Defined per deployment mode
- Recovery Time Objective (RTO): Defined per deployment mode

Targets are agreed with customers for BYOC and On-Prem.

---

## Tenant Isolation During Recovery

- Tenants are recovered independently where possible
- Partial tenant recovery is supported
- Cross-tenant data contamination is explicitly prevented

---

## Testing & Drills

- Restore tests performed regularly
- Full disaster recovery drills scheduled periodically
- Drill outcomes documented
- Gaps result in corrective actions

Untested recovery paths are treated as failures.

---

## Security Considerations

- Backup access tightly controlled
- Backup encryption keys protected
- Restore operations audited
- Sensitive data handled according to compliance rules

---

## On-Prem Specific Considerations

- Customer defines storage and retention policies
- Platform provides validated procedures
- Clear division of responsibility documented
- Offline and air-gapped scenarios supported

---

## Anti-Patterns Explicitly Prevented

- Untested backups
- Manual, undocumented recovery
- Single-backup reliance
- Assuming indexes are authoritative
- Recovering without validation

---

## Outcome

With this strategy:
- Data loss risk is minimized
- Recovery is predictable
- Trust is preserved during failures
- Platform continuity is ensured

---

## Status

This document defines the authoritative backup, restore, and disaster recovery
strategy for EAVIP. All deployments must align with this strategy.
