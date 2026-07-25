# Execution Plan

The execution plan determines work item execution order and extracts the specific upstream artifact sections each work item needs during the four-phase execution loop (Tests → Plan → Code → Review).

## Document Control

| Field | Value |
|-------|-------|
| Artifact ID | EP-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Date | |
| Governance Model Version | 1.0 |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |
| Related Links | |

## Baseline Metrics (Pre-Execution)

- Tests: {count} passing, 0 failing
- Build: clean (zero errors)

## Execution Order

### Work Group {n}: {Group Name}

| Order | WDD Item ID | Intent | Dependencies | Parallel-Safe |
|-------|-------------|--------|--------------|---------------|
| {n} | {WDD item ID} | {summary} | {item IDs or "None"} | Yes / No ({reason if no}) |

{Repeat for each work group}

### Dependency Graph

{Description or diagram of dependency relationships between work items}

## Execution Checklist

### Work Group {n}: {Group Name}

**{WDD Item ID} — {item intent summary}**
- [ ] **Phase 1 (Tests):** Generate test specifications → save as `{nn}-{wdd-item-id}-tests.md`
- [ ] **Phase 2 (Plan):** Generate implementation plan → save as `{nn}-{wdd-item-id}-plan.md`
- [ ] **Phase 3 (Code):** Implement plan, tests pass
- [ ] **Phase 4 (Review):** Review implementation → save as `{nn}-{wdd-item-id}-review.md`

{For human-assigned items:}

**{WDD Item ID} — {item intent summary} [HUMAN]**
- [ ] **Execute:** Human performs work per WDD item scope
- [ ] **Verify:** Complete verification checklist from acceptance criteria
- [ ] **Evidence:** Record evidence for each checklist item
- [ ] **Review:** Another human reviews evidence against DoD

### Work Group {n} Gate

- Tests: {count} passing, 0 failing
- Test count delta: +{n} from previous gate
- Build: clean (zero errors)
- Items completed: {list of WDD Item IDs}
- Reviews: all PASS
- Regression check: no failures in tests from prior work groups
- Evidence: {link or path to test results}

{Repeat checklist and gate for each work group}

---

# Phase Output Templates

## Phase 1: Test Specifications

### {WDD Item ID} — Test Specifications

#### Acceptance Tests

**Test: {descriptive name in Given/When/Then style}**
- Preconditions: {setup state}
- Input: {test input}
- Expected Outcome: {what should happen}
- Failure Condition: {what constitutes failure}

#### Failure Tests

**Test: {descriptive name}**
- Preconditions: {setup state}
- Input: {invalid or edge-case input}
- Expected Outcome: {expected failure behavior}
- Failure Condition: {what constitutes failure}

#### Edge Case Tests

{As above, for boundary conditions}

#### Test Structure

- Test file path: {path following project conventions}
- Test grouping: {groups mapped to acceptance criteria}

---

## Phase 2: Implementation Plan

### {WDD Item ID} — Implementation Plan

#### Plan Summary
{One-paragraph summary of the implementation approach}

#### Files to Change

| File | Action | Changes | Reason |
|------|--------|---------|--------|
| {path} | Create / Modify | {what changes} | {why} |

#### Interfaces Locked

| Interface | Signature | Return Type | Contract |
|-----------|-----------|-------------|----------|
| {name} | {parameters} | {type} | {data contract} |

#### Dependencies
{New dependencies required (verified) or "None"}

#### Risks and Assumptions
- {risk or assumption}

#### Sequencing
{Order of implementation if it matters, or "No ordering constraints"}

---

## Phase 4: Review Report

### {WDD Item ID} — Review

#### Review Summary
{One-sentence verdict: PASS / CONCERNS / BLOCKED}

#### Scope Adherence
{Does the diff match the WDD work item? Any additions?}

#### Interface Compliance
{Do signatures, return types, and contracts match TDD?}

#### Test Coverage
{Are acceptance criteria covered? Failure conditions? Edge cases?}

#### Code Quality
{Error handling? Hardcoded values? Unbounded operations? Dead code? Dependency drift?}

#### Security
{ACF guardrails respected? Secrets exposed? Injection risks?}

#### Verification
{All tests passing? DoD satisfied? Evidence present?}

#### Risks
{Factual risks only — or "None identified"}

#### Blockers
{Issues that must be resolved before merge — or "None"}
