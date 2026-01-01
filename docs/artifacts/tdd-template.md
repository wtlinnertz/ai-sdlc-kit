# TDD Template (Technical Design Document)

## 0. Document Control
- System / Component Name:
- TDD ID:
- Author:
- Date:
- Status: Draft | Approved | Frozen
- Upstream Artifacts:
  - SAD ID / Link:
  - ACF ID / Link (if applicable):
  - DCF ID / Link:
- Related ADRs:

## 1. Intent Summary (Paste Approved Pre-Pass)
Paste the approved Intent Summary here verbatim.
Do not restate or expand it.

## 2. Scope and Non-Goals (Hard Boundary)

### In Scope
- Item 1:
- Item 2:

### Explicit Non-Goals (Must align with SAD)
- Non-goal 1:
- Non-goal 2:

## 3. Technical Overview
Describe the design at a level sufficient to build.
- Components involved:
- Key flows:
- Data movement (high level):

## 4. Interfaces and Contracts (Hard)
For each interface:
- Name:
- Inputs (schemas / parameters):
- Outputs (schemas / results):
- Error modes:
- Versioning expectations (if applicable):

## 5. Build and Deployment Approach (Deterministic)
- Build steps (high level but explicit):
- Deployment steps (high level but explicit):
- Configuration inputs required:
- Secrets required (names only; no values):

Rule: If an engineer/AI would ask a question, this section is incomplete.

## 6. Failure Handling and Rollback (Hard)
- Failure modes:
- Detection signals:
- Rollback or compensation behavior:
- Partial failure behavior:

## 7. Observability (Hard)
Define what must be observable.
- Logs:
- Metrics:
- Traces (if applicable):
- Evidence required to prove success:

## 8. Testing Strategy (Hard)
Define tests and gates.
- Unit tests:
- Integration tests:
- System/acceptance tests:
- Failure tests (at least one):
- Pass/fail criteria:

## 9. Operational Notes (Minimum Runbook)
- Deploy procedure:
- Verify procedure:
- Rollback procedure:
- Ownership/On-call expectations (generic):

## 10. Dependencies
List required dependencies. If none, state “None”.
- Dependency 1:
- Dependency 2:

## 11. Risks and Assumptions
- Risks:
- Assumptions:

## 12. Readiness Checklist (Self-Check)
- [ ] Scope and non-goals explicit and aligned with SAD
- [ ] Interfaces and contracts explicit
- [ ] Build/deploy steps deterministic
- [ ] Failure and rollback behavior defined
- [ ] Tests defined with pass/fail criteria
- [ ] No unresolved decisions

## 13. Freeze Declaration (when ready)
This TDD is approved and frozen. Downstream artifacts may not reinterpret or expand this design.

- Approved By:
- Date:
