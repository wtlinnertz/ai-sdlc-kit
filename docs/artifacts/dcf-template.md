# DCF Template (Design Context File)

The DCF defines **design standards and expectations** that constrain TDD creation.
It is reusable across many initiatives.

## 0. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | DCF-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Date | |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |
| Applies To | (e.g., “All delivery designs”, “This platform only”) |

## 1. Purpose
What design-level standards does this DCF enforce?

## 2. Design Principles (Hard)
Examples:
- Prefer deterministic designs over exploratory steps
- Design for rollback and failure
- Make interfaces explicit
- Prefer smallest safe change

List your principles:
- Principle 1:
- Principle 2:

## 3. Quality Bars (Hard)
Minimum expectations that must be met in the TDD.
- Interfaces and contracts must be explicit
- Failure and rollback behavior must be defined
- Tests must be defined with pass/fail criteria
- Operability must be documented

Add your own:
- Quality bar 1:
- Quality bar 2:

## 4. Non-Goals Enforcement (Hard)
- TDD must explicitly restate non-goals from SAD
- TDD must not implement excluded functionality
- “Helpful” scope expansion is not allowed

## 5. Operational Expectations (Hard)
- Deployment verification expectations:
- Monitoring/alerting expectations (what must be observable):
- Auditability expectations:

## 6. Testing Expectations (Hard)
- Required test layers:
- Evidence requirements (logs, reports, artifacts):
- Promotion gates (what blocks progression):

### Evidence Management
Define how evidence is handled for audit and compliance:
- Required evidence formats: (e.g., structured logs, test reports, screenshots)
- Evidence storage location: (e.g., artifact repository, document management system)
- Retention requirements: (e.g., 1 year for test results, 7 years for compliance records)
- Accessibility requirements: (e.g., retrievable within 24 hours for audit)

## 7. Documentation Expectations (Hard)
- Required sections in a TDD:
- Required diagram types (if any):
- Required traceability markers:

## 8. Open Items
- Open item 1:
- Open item 2:

## 9. Freeze Declaration (when ready)
This DCF is approved and frozen. All TDDs must comply.

- Approved By:
- Date:
