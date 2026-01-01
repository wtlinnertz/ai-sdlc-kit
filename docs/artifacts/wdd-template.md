# WDD Template (Work Design Document)

Translate a frozen TDD into **atomic, executable work items** suitable for AI agents or humans.

## 0. Document Control
- WDD ID:
- Author:
- Date:
- Status: Draft | Approved | Frozen
- Parent TDD:
  - TDD ID / Link:
  - TDD Status: Frozen (required)

## 1. Scope and Non-Goals (Copied from TDD)
Paste the TDD scope and non-goals here verbatim (or link to exact section).
Do not restate or expand.

## 2. Work Items

Repeat this section for each work item.

### WDD Item
- WDD Item ID:
- Parent TDD Section:
- Assignee Type: AI Agent | Human | Either

#### Intent (1–2 sentences)
Exactly what this work item accomplishes.

#### In Scope
- Bullet list

#### Out of Scope / Non-Goals
- Bullet list (must align with TDD)

#### Inputs
- Configs, parameters, manifests, approvals, secrets (names only)

#### Outputs
- Files, resources, state changes, evidence/logs

#### Acceptance Criteria (Executable)
Use Given/When/Then.
Include at least one failure condition.
- AC1:
- AC2:

#### Dependencies
List dependencies or state “None”.
- Dependency 1:

#### Rollback / Failure Behavior
What happens if this fails? What is rolled back or compensated?

---

## 3. Mandatory Granularity Rules (Hard)

Every WDD item must satisfy all of the following:

- One observable outcome
- One pull request
- One subsystem or repo
- No design decisions
- No cross-environment deployment
- Completable in a short, bounded time window

Items violating these rules must be split.

---

## 4. Freeze Declaration (when ready)
This WDD is approved and frozen. Jira story generation may proceed.

- Approved By:
- Date:
