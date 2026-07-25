# WDD Template (Work Design Document)

Translate a frozen TDD into **atomic, executable work items** suitable for AI agents or humans.

## 0. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | WDD-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Author | |
| Date | |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

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
- Required Capabilities: (e.g., backend, database, API-design, security)
- Complexity Estimate: S | M | L — (one-sentence justification)

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
Include at least one failure condition per acceptance criterion.
- AC1:
- AC2:

#### Definition of Done (Hard)
- [ ] PR merged
- [ ] Tests passing (type specified)
- [ ] Evidence/logs generated

#### Interface Contract References
List TDD §4 contracts this item implements or consumes. State role (provider or consumer).
Omit or state "None" if internal to a single component.
- Contract 1:

#### Dependencies
List dependencies or state "None".
- Dependency 1:

#### Rollback / Failure Behavior
What happens if this fails? What is rolled back or compensated?

---

## 3. Work Groups (Optional)

Group related work items that together deliver a **business-testable capability**. Work groups enable incremental business acceptance testing before the entire TDD is complete.

### Work Group
- Group ID:
- Group Name:
- Business Capability: (what becomes testable when all items in this group are complete)
- Member Items: (list WDD Item IDs)
- Acceptance Criteria (Group-Level): (business-level criteria verifiable after all member items are done)

Repeat for each group. Every work item should belong to exactly one group. Items that are independently testable may form a single-item group.

---

## 4. Freeze Declaration (when ready)
This WDD is approved and frozen. Execution may proceed.

- Approved By:
- Date:
