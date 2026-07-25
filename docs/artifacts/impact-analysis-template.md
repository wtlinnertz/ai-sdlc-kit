# Impact Analysis Report

The impact analysis assesses the downstream ripple effects of a proposed change to a frozen SDLC artifact. It maps what is affected and how severely, enabling informed re-entry decisions.

## Document Control

| Field | Value |
|-------|-------|
| Artifact ID | IA-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Date | |
| Proposed Change Source | {addendum draft / change description / bug report / feature request} |
| Governance Model Version | 1.0 |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

## Change Target
- Target Artifact: {artifact type and ID being changed}
- Sections Affected: {list of sections in the target artifact that would change}

## Impact Assessment

### Downstream Artifact Impact

| Artifact | Sections Affected | Severity | Reason |
|----------|-------------------|----------|--------|
| {artifact type and ID} | {sections that reference changed content} | must_revise / review_recommended / likely_unaffected | {why this artifact is affected} |

### Work Item Impact

| Work Item ID | Execution Status | Severity | Reason |
|--------------|------------------|----------|--------|
| {WDD item ID} | not_started / in_progress / completed / unknown | must_revise / review_recommended | {why this work item is affected} |

### Constraint Impact

| Source Constraint | Affected Artifact | Propagating Constraint | Severity |
|-------------------|-------------------|------------------------|----------|
| {ACF/DCF section} | {downstream artifact} | {specific constraint} | must_revise / review_recommended |

{If no constraint impact: "No ACF or DCF constraints are affected by this change."}

### Non-Goal Impact

| Non-Goal | Affected Artifact | Scope Boundary | Severity |
|----------|-------------------|----------------|----------|
| {PRD non-goal reference} | {downstream artifact} | {specific boundary} | must_revise / review_recommended |

{If no non-goal impact: "No PRD non-goals are affected by this change."}

### Addendum Cascade

| Downstream Artifact | Addendum ID | Conflict Description |
|----------------------|-------------|----------------------|
| {artifact with frozen addendum} | {addendum ID} | {conflict with proposed change} |

{If no addendum conflicts: "No downstream addendums conflict with this change." If no downstream addendums exist: "No downstream addendums exist."}

## Hard Gate Results

| Gate | Result |
|------|--------|
| downstream_artifact_impact | PASS / FAIL |
| work_item_impact | PASS / FAIL |
| constraint_impact | PASS / FAIL |
| non_goal_impact | PASS / FAIL |
| addendum_cascade | PASS / FAIL |

## Decision

- **Status:** IMPACT / NO_IMPACT
- **Re-entry Required:** Yes / No
- **Estimated Cascade Depth:** {number of artifact chain levels affected}

## Warnings

{Non-blocking observations, including missing downstream artifacts.}

- {warning 1}
- {warning 2}

{If none: "No warnings."}
