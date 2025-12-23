# Document Management, Indexing & Search

## Purpose

This document defines the **authoritative document management model**
for the Enterprise Architecture Visibility & Intelligence Platform (EAVIP).

It explains how architectural documents (MD, Word, PDFs) are:
- Stored
- Indexed
- Linked to architecture entities
- Searched
- Governed
- Versioned

This is the **knowledge-management contract** for the platform.

## Core Document Principles (Locked)

1. Documents are first-class architecture artifacts
2. No document exists without context
3. Documents are immutable once approved
4. Indexing is automatic and transparent
5. Search must work across structure and content
6. Documentation scales without chaos

## Supported Document Types

EAVIP supports:

- Markdown (primary, preferred)
- Word documents
- PDF files
- Plain text
- Images (diagrams, screenshots)

Markdown is the **source-of-truth format** wherever possible.

## Document Context Model

Every document must be attached to **at least one** entity:

- Enterprise
- Organization
- Application
- Component
- Dependency
- Governance item (ADR, policy, decision)

A document without context is rejected.

## Document Categories (Authoritative)

- Architecture Decision Records (ADR)
- High-Level Design (HLD)
- Low-Level Design (LLD)
- Integration Design
- Data Model / ER
- Security Design
- Compliance Evidence
- Operational Runbooks
- Reference Material

Categories drive indexing and visibility.

## Document Lifecycle

Draft  
→ Review  
→ Approved  
→ Superseded (optional)  

Rules:
- Drafts are editable
- Approved documents are immutable
- Superseded documents remain searchable
- Deletions are forbidden (only expiration)

## Versioning Model

- Every update creates a new version
- Previous versions remain accessible
- Versions are time-context aware
- Diagrams and decisions reference document versions explicitly

## Indexing Model

Documents are indexed on:

- Title
- Category
- Entity linkage
- Content (full-text)
- Tags
- Author
- Approval status
- Time validity

Indexing is **automatic and asynchronous**.

## Search Capabilities

Search supports:

- Full-text search
- Entity-scoped search
- Category-based filtering
- Tag-based filtering
- Time-context filtering

Examples:
- “Show all ADRs for Payments Application”
- “Find documents mentioning Kafka”
- “Security designs approved last quarter”

## Tagging Strategy

Documents can be tagged with:
- Technology
- Domain
- Risk level
- Compliance area
- Transformation initiative

Tags are normalized, not free-text.

## Document Navigation

From any entity screen, users can:
- View linked documents
- Filter by category
- Jump directly to document sections
- Navigate from document → entity → diagram

Documents and diagrams are always connected.

## Access Control

Document access follows:
- Entity permissions
- Role-based access
- Approval state

Sensitive documents can be:
- Restricted
- Redacted
- Role-limited

## Governance Integration

Documents can:
- Trigger governance workflows
- Be required for approvals
- Act as compliance evidence

Approval of certain changes may mandate:
- ADR attachment
- Design document attachment

## Audit & Traceability

For every document:
- Creation author is recorded
- Reviewers are recorded
- Approval decision is recorded
- Version history is immutable

Documents are audit artifacts.

## Storage Model

- Object storage abstraction
- Metadata in relational store
- Index in search engine abstraction

No document content is stored inline in the graph.

## What This Model Avoids

- Wiki sprawl
- Orphaned documents
- Out-of-date designs
- Tribal knowledge
- Manual indexing

## Outcome

With this document management model:
- Architecture knowledge stays organized
- Searching replaces browsing
- Documents remain trustworthy
- Scale does not create entropy
- GitHub and EAVIP stay aligned

## Status

This document defines the **authoritative document management, indexing, and search model**.
All documentation handling must conform to this design.
