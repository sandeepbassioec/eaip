# Frontend Reference Architecture – Skeleton Implementation
## Enterprise Architecture Visibility & Intelligence Platform (EAVIP)

---

## Purpose

This document defines the **frontend reference architecture** for EAVIP,
aligned with:

- TOGAF execution intent
- DDD bounded contexts
- Modular Monolith backend
- Walking Skeleton approach

It ensures the frontend:
- Reflects architecture, not just UI
- Respects bounded contexts
- Remains evolvable as capabilities grow
- Does not become a “god UI”

This is the **canonical frontend blueprint** for all future development.

---

## Core Principle (Locked)

**Frontend must mirror architectural boundaries, not hide them.**

If the UI collapses boundaries, backend discipline will erode.

---

## Technology Stack (Locked for Phase-1)

- Framework: **React**
- Language: **TypeScript**
- State Management: **Context + Hooks (initially)**
- Routing: **React Router**
- Data Fetching: **Fetch / Axios (thin abstraction)**
- Forms: **React Hook Form**
- Validation: **Shared DTO validation**
- Styling: **CSS Modules / Tailwind (choice flexible)**
- Build Tooling: **Vite**
- Testing: **Jest + React Testing Library**

No UI framework lock-in at this stage.

---

## Frontend Architectural Style

### Chosen Style

**Architecture-Aware Modular UI**

This means:
- UI modules align with backend bounded contexts
- No global “feature soup”
- Explicit ownership of screens and flows

---

## Frontend Module Structure

/src
/architecture-core
/pages
/components
/api
/models
/state

/governance
/metrics
/visualization
/platform-config

/shared
/app


---

## Module Ownership Rules

Each frontend module:
- Maps to exactly one bounded context
- Owns its screens, state, and API clients
- Must not directly import another context’s internals

Cross-context interaction is **explicit and intentional**.

---

## Shared Layer (Very Small)

Allowed:
- UI primitives (buttons, inputs)
- Layout components
- Routing shell
- Auth utilities
- Typed HTTP client

Forbidden:
- Business logic
- Context-specific state
- API orchestration

Shared ≠ dumping ground.

---

## API Client Strategy

- One API client per bounded context
- Typed request/response DTOs
- No domain logic in API clients
- Errors normalized at boundary

Example:
- `architectureCoreApi.createApplication()`

---

## State Management Strategy

### Phase-1 (Skeleton)

- Local state via hooks
- Context only where necessary
- No global Redux-like store

### Why

- Reduces accidental coupling
- Keeps flows understandable
- Matches small scope of skeleton

Advanced state management comes **after clarity**, not before.

---

## Walking Skeleton UI Flow

### Selected Flow
**Create Application**

UI Steps:
1. Navigate to Organization
2. Open “Create Application”
3. Enter application name
4. Submit
5. Display success state

This validates:
- Routing
- API integration
- State handling
- Error display
- Boundary discipline

---

## Error Handling & UX Rules

- Domain errors are user-visible
- Technical errors are generic
- No stack traces
- Clear actionable feedback

UX clarity is part of architecture quality.

---

## Security Considerations

- Token handling isolated
- No business decisions in UI
- Authorization enforced server-side
- UI adapts to permissions, not enforces them

Security is **defensive by design**.

---

## Testing Strategy

### Unit Tests
- Components
- Hooks
- UI logic

### Integration Tests
- Page flows
- API interactions (mocked)

No snapshot-heavy testing.

---

## Trade-offs (Explicit)

### Pros
- Clear mental model
- Strong alignment with backend
- Easy scaling
- Boundary protection

### Cons
- More folders
- Requires discipline
- Slight upfront structure cost

Accepted intentionally.

---

## Why This Frontend Works for EAVIP

- Reinforces architecture thinking
- Prevents UI-driven coupling
- Scales with platform complexity
- Enables diagram-heavy future UX

This UI can grow safely with the platform.

---

## Final Mental Model

- UI is an architectural citizen
- Boundaries are visible
- Simplicity before sophistication
- Learning before optimization

---

## Next Step

Proceed to **Platform Bootstrap & Repository Initialization**

File:`ea/platform-bootstrap.md`
