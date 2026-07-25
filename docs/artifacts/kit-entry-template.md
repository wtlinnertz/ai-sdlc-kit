# EEK Kit Entry Record

A lightweight gate that must be completed and frozen before beginning artifact generation in the Engineering Execution Kit.

This record is **human-authored**. It is validated against `kit-entry-spec.md` before the PRD entry path begins.

---

## Document Control

| Field | Value |
|-------|-------|
| Artifact ID | KER-{YYYY}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Date | |
| Initiated By | |
| Work Summary | (1-2 sentences describing what this EEK engagement will deliver) |
| Governance Model Version | 1.0 |
| Prompt Version | N/A |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

---

## Classification Check

Select one:

- [ ] **Classification record exists** — Work Classification Record ID: _____________
  Confirm the record routes to: Engineering Execution Kit
- [ ] **No classification record** — Justification for absence:
  _(Must be specific. State why classification was not performed — e.g., "Bug fix routed directly from incident response; classification not applicable." Generic statements such as "N/A" or "skipped" are not accepted.)_

---

## Entry Path

Select exactly one:

- [ ] **Path A — Discovery Entry**
  Frozen DPRD reference (document ID, file path, or link): _____________

  EL experiment references (EXP-N) present in DPRD Assumptions section:
  - [ ] Yes — EXP-N references are present for tested assumptions
  - [ ] No — Explanation: _____________
  _(Required. If No, state why EL references are absent — e.g., "All assumptions were validated as established facts before discovery; no experiments were conducted." Blank is not accepted.)_

- [ ] **Path B — Direct Entry (discovery bypassed)**
  Work type:
  - [ ] Bug Fix
  - [ ] Tech Debt
  - [ ] Compliance Mandate
  - [ ] Other: _____________

  Justification for bypassing discovery:
  _(Must be specific and consistent with the work type selected above — e.g., "Bug Fix: reproduction steps confirmed in staging; no design decision required; no user-facing behavior change beyond restoring correct function." Vague rationale such as "small change" or "no time" is not accepted.)_

---

## SSK Disposition

SSK disposition:
- [ ] Path B entry — SSK not applicable
- [ ] SSK was engaged — SDR ID: {SDR-ID}, status: Frozen
- [ ] SSK was skipped — Justification: {specific reason why Build is the only option}

_(Path A KERs must select one of the SSK engaged or SSK skipped options and provide the required detail. Path B KERs must select "Path B entry — SSK not applicable." Skipped justifications must explain why Build is the only viable option — not vendor preference or time pressure.)_

---

## Priority Decision

- Priority decision on record: Yes / No
- Reference (date + approver name, planning session, or tracking system ID): _____________

---

## Scope Boundary

State what this work covers and what it does not:

**In scope:** (1-3 sentences)

**Out of scope:** (1-3 sentences — what related work is explicitly excluded)

---

## Completeness Checklist

Before validating and freezing this record, confirm:

- [ ] Record ID and date are present
- [ ] Classification check is complete (record referenced or absence justified)
- [ ] If classification record exists, it routes to EEK
- [ ] Exactly one entry path is selected
- [ ] Path A: DPRD reference is provided
- [ ] Path A: EL experiment references field is completed (Yes or No with explanation)
- [ ] Path B: work type is explicitly selected
- [ ] Path B: specific justification is documented and consistent with work type
- [ ] SSK disposition is declared (Path A: engaged or skipped with justification; Path B: not applicable)
- [ ] Priority decision has a traceable reference
- [ ] Scope boundary states both in scope and out of scope

---

## Freeze Declaration

This Kit Entry Record is validated and frozen. Artifact generation may proceed.

- Validated Against: `kit-entry-spec.md`
- Validation Result: PASS
- Frozen By:
- Date:
