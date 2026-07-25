# Definition of Ready (DoR) Check

The DoR evaluates whether a WDD work item is complete and unambiguous enough to begin execution. It is a per-item readiness gate.

## Document Control

| Field | Value |
|-------|-------|
| Artifact ID | DoR-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| WDD Item ID | {WDD item ID being evaluated} |
| Date | |
| Governance Model Version | 1.0 |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

## Work Item Under Evaluation

- **Item ID:** {WDD item ID}
- **Intent:** {one-line summary of the work item}
- **Assignee Type:** AI Agent / Human / Either

## Readiness Checks

### 1. Traceability
- **WDD Item ID:** {present / missing}
- **TDD Section Reference:** {present / missing / "TBD"}

### 2. Atomic Scope
- **Single outcome:** {yes / no — describe if compound}

### 3. Acceptance Criteria
- **Format:** {Given/When/Then (AI) / Verification checklist (Human)}
- **Format matches Assignee Type:** {yes / no}
- **Failure conditions present:** {yes / no — list any criteria missing failure conditions}

### 4. Inputs and Outputs
- **Inputs explicitly listed:** {yes / no}
- **Outputs explicitly listed:** {yes / no}
- **Hidden dependencies detected:** {none / list}

### 5. Definition of Done
- **PR merged criterion:** {present / missing}
- **Tests passing criterion:** {present / missing — test type specified?}
- **Evidence requirement:** {present / missing}

### 6. Dependencies
- **Dependencies:** {explicitly listed / "None" declared / missing}

### 7. Execution Ownership
- **Assignee Type:** {AI Agent / Human / Either / missing}

### 8. AI Safety
- **Open-ended language:** {none / list instances}
- **Unresolved decisions (TBD):** {none / list instances}
- **Undocumented assumptions:** {none / list instances}

### 9. Granularity
- **Single outcome:** {yes / no}
- **Single repo/subsystem:** {yes / no}
- **Single PR feasible:** {yes / no}
- **Cross-environment execution:** {no / yes — describe}

### 10. Rollback / Failure Behavior
- **Failure behavior defined:** {yes / no / TBD}
- **Rollback approach stated:** {yes / no / TBD}

## Hard Gate Results

| Gate | Result |
|------|--------|
| traceability | PASS / FAIL |
| atomic_scope | PASS / FAIL |
| acceptance_criteria | PASS / FAIL |
| inputs_outputs | PASS / FAIL |
| definition_of_done | PASS / FAIL |
| dependencies | PASS / FAIL |
| execution_ownership | PASS / FAIL |
| ai_safety | PASS / FAIL |
| granularity | PASS / FAIL |
| rollback_behavior | PASS / FAIL |

## Decision

- **Status:** PASS / FAIL
- **Completeness Score:** {0-100}

## Blocking Issues

| Gate | Description | Location |
|------|-------------|----------|
| {gate name} | {factual, actionable issue} | {section reference} |

{If none: "No blocking issues."}

## Warnings

- {warning 1}

{If none: "No warnings."}
