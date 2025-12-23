# Infrastructure & Deployment Reference (IaC + Runtime)

## Purpose

This document defines the authoritative infrastructure and deployment model
for EAVIP, covering SaaS, BYOC, and On-Prem deployments along with
Infrastructure-as-Code, environment separation, and operational guardrails.

This is the execution contract for DevOps and platform engineering.

## Core Infrastructure Principles (Locked)

1. Infrastructure is code
2. Cloud-neutral abstractions
3. Same topology across SaaS, BYOC, and On-Prem
4. No environment-specific logic in application code
5. Operational responsibility follows deployment model
6. Security defaults to deny

## Deployment Models (Authoritative)

### SaaS (Reference Model)
- Operated by EAVIP
- Default reference cloud: AWS
- Multi-tenant
- Highest automation level

### BYOC
- Operated by customer
- Any cloud (AWS, Azure, GCP)
- Tenant-isolated
- Customer owns infrastructure and runtime

### On-Prem
- Operated by customer
- Air-gapped supported
- Limited managed services
- Adapter-based integrations only

## Reference Runtime Topology

Load Balancer  
→ API Gateway  
→ Application Services  
→ Graph Service  
→ Persistence Layer  
→ Event Backbone  

This topology is consistent across all deployment models.

## Infrastructure Abstraction Layers

### Compute
- Kubernetes (preferred)
- Docker (minimum requirement)
- VM-based fallback (on-prem)

### Networking
- Ingress / API Gateway
- Optional service mesh
- mTLS supported

### Persistence
- Graph store abstraction
- Relational store
- Object storage abstraction

### Eventing
- Kafka, RabbitMQ, ActiveMQ
- Cloud equivalents via adapters

## Infrastructure-as-Code Strategy

- Terraform for infrastructure provisioning
- Helm for Kubernetes packaging
- Kustomize for environment overlays

Manual infrastructure changes are forbidden.

## Environment Strategy

Standard environments:
- Dev
- QA
- Staging
- Production

Each environment is:
- Credential-isolated
- Network-isolated
- Data-isolated

## Configuration & Secrets

- Externalized configuration
- Environment variables
- Secret managers (cloud or local)

No secrets in code, git, or container images.

## Networking & Security

### Ingress
- HTTPS only
- TLS termination
- WAF for SaaS and BYOC

### Internal
- mTLS between services
- Network policies enforced
- No flat networks

## Identity & Access (Infrastructure Level)

- OAuth2 / OIDC integration
- Service identities
- Short-lived credentials
- Rotation supported

## Observability (Infrastructure Level)

Required:
- Centralized logging
- Health checks
- Metrics endpoints

Optional (later):
- Distributed tracing
- Alerting
- SLOs

## Backup & Disaster Recovery

### SaaS
- Managed backups
- Cross-region replication

### BYOC / On-Prem
- Customer-managed backups
- Snapshot and restore tooling provided

The event store is the ultimate recovery source.

## Upgrade & Rollout Strategy

- Blue/Green or Canary deployments
- Backward-compatible schema changes
- Feature flags for risky changes
- Zero-downtime upgrades

## What This Model Avoids

- Snowflake environments
- Manual hotfixes
- Vendor lock-in
- Hidden credentials
- One-off scripts

## Outcome

With this infrastructure model:
- Deployments are predictable
- Security posture is consistent
- SaaS and On-Prem share the same DNA
- Operations scale cleanly
- Failures are recoverable

## Status

This document defines the authoritative infrastructure and deployment reference.
All DevOps and platform work must conform to this model.
