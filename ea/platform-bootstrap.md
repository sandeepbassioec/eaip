# Platform Bootstrap & Repository Initialization
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines **how the EAVIP platform is bootstrapped from zero**
into a **running, governed, architecture-first codebase**.

It answers:
- How repositories are initialized
- How architecture rules are enforced from Day-0
- How developers start without breaking boundaries
- How CI/CD and quality gates protect architectural intent

This is the **entry point for real execution**.

---

## Core Principle (Locked)

**The first commit decides the future quality of the system.**

If the bootstrap is weak:
- Architecture erodes silently
- Rules become “guidelines”
- Discipline disappears

---

## Repository Strategy (Locked)

### Chosen Strategy

**Single Monorepo with Enforced Modular Boundaries**

Why:
- Enables fast iteration
- Simplifies refactoring
- Keeps architectural context visible
- Matches Modular Monolith strategy

Multi-repo comes later, by extraction — not by guessing.

---

## Repository Layout (Authoritative)

/ea
/docs
index.md

/src
/EAVIP.Architecture.Core
/EAVIP.Architecture.Governance
/EAVIP.Architecture.Metrics
/EAVIP.Architecture.Visualization
/EAVIP.Platform.Configuration
/EAVIP.SharedKernel
/EAVIP.Host

/tests
/Architecture.Tests
/Domain.Tests
/Integration.Tests

/build
/ci
/scripts


No other top-level folders are allowed.

---

## Solution Initialization Steps

### Step 1 – Create Solution

```bash
dotnet new sln -n EAVIP
dotnet new classlib -n EAVIP.Architecture.Core
dotnet new classlib -n EAVIP.Architecture.Governance
dotnet new classlib -n EAVIP.Architecture.Metrics
dotnet new classlib -n EAVIP.Architecture.Visualization
dotnet new classlib -n EAVIP.Platform.Configuration
dotnet new classlib -n EAVIP.SharedKernel
dotnet new webapi   -n EAVIP.Host
```

Add all projects to the solution.

##Dependency Guardrails (MANDATORY)
###Allowed References
* API → Application
* Application → Domain
* Infrastructure → Application + Domain
* Host → API only

###Forbidden References
* Domain → Infrastructure
* Domain → Application
* Cross-bounded-context domain references

These are enforced via architecture tests.
---
##Architecture Tests (Non-Negotiable)
###Purpose
Prevent accidental dependency violations.

###Tooling
* NetArchTest / ArchUnit-style tests
* Executed in CI

###Example Rules
* Domain must not reference EF Core
* SharedKernel must not reference domain projects
* No project references another bounded context directly

If tests fail → build fails.
---
CI/CD Bootstrap
Minimum CI Pipeline (Day-1)
* Restore dependencies
* Build solution
* Run unit tests
* Run architecture tests
* Package artifacts

No CI = no merge.
---
Local Developer Experience
Developer Onboarding Script
* Clone repo
* Run dotnet build
* Run dotnet test
* Run dotnet run (Host)

If this fails, architecture adoption fails.
---
Configuration Strategy
*  Environment-based configuration
*  No secrets in repo
*  Support for:
   *  Local dev
   *  CI
   *  SaaS
   *  BYOC
   *  On-Prem

Secrets resolved via provider adapters.
---
Database Bootstrap (Skeleton Phase)
*  Local PostgreSQL / SQL Server
*  One schema per bounded context
*  Migration projects per context
*  No cross-schema joins

Migration ownership is strict.
---
Logging & Observability (Minimal)
*  Structured logging
*  Correlation IDs
*  Request tracing

Advanced observability comes later.
---
Governance Hooks (Day-1)
*  Architecture tests mandatory
*  ADR creation required for:
   *  New bounded contexts
   *  New integrations
   *  Cross-context changes

Governance starts immediately.
---

Trade-offs (Explicit)
Pros
*  Clean start
*  Enforced discipline
*  Predictable evolution
*  Developer clarity

Cons
*  Initial setup cost
*  Requires buy-in
*  Less flexibility early

Accepted intentionally.
---
Why This Bootstrap Works
* Prevents architectural erosion
* Aligns engineering with architecture
* Scales with team size
* Enables safe experimentation

This is how real enterprise platforms begin.
---

Final Mental Model
* First commit is sacred
* Structure beats convention
* Guardrails > guidelines
* Architecture is executable

File: `ea/developer-workflow-and-adrs.md`
