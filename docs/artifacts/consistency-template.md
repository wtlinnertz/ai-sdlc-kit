# Consistency Check Report

The consistency check verifies that intent, requirements, constraints, and scope flow consistently from upstream artifacts to downstream artifacts without gaps, contradictions, or unauthorized expansion.

## Document Control

| Field | Value |
|-------|-------|
| Artifact ID | CC-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Date | |
| Governance Model Version | 1.0 |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

## Artifacts Checked

| Artifact | Status | Notes |
|----------|--------|-------|
| PRD | Present / Missing | |
| ACF | Present / Missing | |
| SAD | Present / Missing | |
| DCF | Present / Missing | |
| TDD | Present / Missing | |
| WDD | Present / Missing | |

## Traceability Matrix

### Requirement Coverage (PRD → SAD)

| Requirement ID | SAD Component | Status |
|----------------|---------------|--------|
| {FR/NFR ID} | {SAD component or "UNTRACED"} | Traced / Untraced |

- **Total requirements:** {count}
- **Traced:** {count}
- **Untraced:** {list of untraced requirement IDs}

### Requirement-to-Work Traceability (PRD → WDD)

| Requirement ID | WDD Work Item(s) | Status |
|----------------|-------------------|--------|
| {FR ID} | {WDD item IDs or "UNTRACED"} | Traced / Untraced |

- **Total functional requirements:** {count}
- **Traced to work items:** {count}
- **Untraced:** {list}

### Orphaned Work Items (WDD → PRD)

| WDD Item ID | Traces To | Status |
|-------------|-----------|--------|
| {WDD item ID} | {requirement ID or "NONE"} | Traced / Orphaned |

- **Total work items:** {count}
- **Traced:** {count}
- **Orphaned (phantom scope):** {list}

## Consistency Checks

### 1. Requirement Coverage
{Assessment of PRD requirement → SAD component coverage}

### 2. Requirement-to-Work Traceability
{Assessment of PRD requirement → WDD work item coverage}

### 3. Scope Containment
{Assessment of downstream scope vs. upstream authorization}

### 4. Non-Goal Enforcement
| Non-Goal | Downstream Violations |
|----------|----------------------|
| {PRD non-goal} | {violating artifact and section, or "None"} |

### 5. Constraint Propagation
| ACF/DCF Constraint | Downstream Violations |
|---------------------|----------------------|
| {constraint} | {violating artifact and section, or "None"} |

### 6. Interface Alignment
| SAD Integration Point | TDD Specification | Status |
|------------------------|-------------------|--------|
| {SAD interface} | {TDD specification} | Aligned / Mismatched |

### 7. Addendum Integration
| Addendum | Downstream Integration | Status |
|----------|------------------------|--------|
| {artifact addendum ID} | {downstream reflection} | Integrated / Unintegrated |

{If no addendums exist: "No frozen addendums exist."}

### 8. Boundary Consistency
| SAD Boundary | TDD Specification | Status |
|--------------|-------------------|--------|
| {boundary, data ownership, or failure mode} | {TDD specification} | Consistent / Inconsistent |

## Inconsistencies

| # | Type | Description | Upstream | Downstream |
|---|------|-------------|----------|------------|
| 1 | dropped_requirement / phantom_scope / contradiction / non_goal_violation / constraint_violation | {description} | {artifact, section} | {artifact, section} |

{If none: "No inconsistencies found."}

## Hard Gate Results

| Gate | Result |
|------|--------|
| requirement_coverage | PASS / FAIL |
| requirement_to_work | PASS / FAIL |
| scope_containment | PASS / FAIL |
| non_goal_enforcement | PASS / FAIL |
| constraint_propagation | PASS / FAIL |
| interface_alignment | PASS / FAIL |
| addendum_integration | PASS / FAIL |
| boundary_consistency | PASS / FAIL |

## Decision

- **Status:** PASS / FAIL
- **Consistency Score:** {0-100}

## Warnings

{Non-blocking observations, including missing artifacts.}

- {warning 1}

{If none: "No warnings."}
