# SAD Template (System Architecture Design)

## 0. Document Control
- System Name:
- SAD ID:
- Author:
- Date:
- Status: Draft | Approved | Frozen
- Upstream Artifacts:
  - PRD ID / Link:
  - ACF ID / Link:
- Related ADRs:

## 1. Intent Summary (Paste Approved Pre-Pass)
Paste the approved Intent Summary here verbatim.
Do not restate or expand it.

## 2. Scope and Non-Goals (Hard Boundary)

### In Scope
- Item 1:
- Item 2:

### Explicit Non-Goals
- Non-goal 1:
- Non-goal 2:

Rule: Anything not listed as in-scope is out of scope by default.

## 3. System Context (Black Box)
Describe the system as a black box.

### Responsibilities
- Responsibility 1:
- Responsibility 2:

### External Actors / Systems
- Upstream:
- Downstream:
- Users/Clients:

### Trust Boundaries
- Boundary 1:
- Boundary 2:

## 4. High-Level Architecture (White Box)
Define major components and interactions.

### Major Components
For each component:
- Name:
- Responsibility:
- Key interactions:

### Communication Patterns
- Sync vs async:
- Protocols (high level):
- High-level data flow:

## 5. Key Architectural Decisions
Record only decisions that affect system shape.
Each decision should reference an ADR when applicable.

- Decision:
  - Rationale:
  - Alternatives considered:
  - Consequences:

## 6. Cross-Cutting Concerns (Architectural Handling)

### Security
- Authn/authz posture:
- Data protection posture:

### Reliability and Resilience
- Failure isolation strategy:
- Retry/fallback philosophy:

### Observability
- What must be observable (not how):

### Performance and Scale
- Scaling model (high level):
- Constraints (high level):

## 7. Constraints and Guardrails (from ACF)
List hard constraints that downstream artifacts must respect.
- Guardrail 1:
- Guardrail 2:

## 8. Deferred Decisions (Explicit)
List items intentionally deferred to TDD-level detail.
- Deferred 1:
- Deferred 2:

## 9. Risks and Assumptions

### Risks
- Risk 1:
- Risk 2:

### Assumptions
- Assumption 1:
- Assumption 2:

## 10. Readiness Checklist (Self-Check)
- [ ] Intent Summary pasted and unchanged
- [ ] Scope and non-goals explicit
- [ ] Boundaries and major components clear
- [ ] Decisions resolved or explicitly deferred
- [ ] No implementation details (build steps, configs, pipelines)

## 11. Freeze Declaration (when ready)
This SAD is approved and frozen. Downstream artifacts may not reinterpret or expand this architecture.

- Approved By:
- Date:
