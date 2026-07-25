# ORD Template (Operational Readiness Document)

Verify that operational requirements from the TDD, ACF, and DCF have been implemented and are working before declaring production readiness.

The ORD is an **evidence-gathering artifact** — it does not define new requirements. Every verification item traces to a specific upstream requirement.

## 0. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | ORD-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Author | |
| Date | |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

- Upstream Artifacts:
  - TDD ID / Link:
  - ACF ID / Link:
  - DCF ID / Link:

## 1. Scope
What system or component is being verified?
Restate from TDD §1. Do not expand.

## 2. Evidence Standards

Every evidence item in this document must meet these properties:

- **Concrete** — An artifact (log, report, screenshot, test output), not an assertion ("we tested this")
- **Timestamped** — When the evidence was collected
- **Traceable** — Links back to the specific upstream requirement it satisfies
- **Retrievable** — A location where the evidence can be accessed (URL, path, or system reference)

Evidence format, storage location, and retention requirements are defined in the organization's DCF (§6 Testing Expectations). If the DCF does not specify these, use whatever format is most durable and accessible to the team.

## 3. Deployment Verification
Verify that deployment succeeded as defined in TDD §5 (Build and Deployment Approach).

For each deployment step in the TDD:
- Step:
- Expected outcome:
- Evidence (logs, screenshots, or test results):
- Status: Verified | Not Verified | N/A

## 4. Observability Verification
Verify that observability requirements from TDD §7 and ACF §6 are satisfied.

For each observability requirement:
- Requirement (from TDD/ACF):
- Evidence type (log sample, metric dashboard, trace screenshot):
- Evidence:
- Status: Verified | Not Verified | N/A

## 5. Alerting and Monitoring
Verify that monitoring and alerting expectations from DCF §5 are satisfied.

For each monitoring/alerting expectation:
- Expectation (from DCF):
- Alert or monitor configured:
- Evidence (alert definition, test fire result):
- Status: Verified | Not Verified | N/A

## 6. Failure and Rollback Verification
Verify that failure handling works as designed in TDD §6 (Failure Handling and Rollback).

For each failure mode in the TDD:
- Failure mode:
- Expected behavior:
- Evidence (test result, simulation log):
- Status: Verified | Not Verified | N/A

## 7. Security Verification
Verify that security guardrails from ACF §3 are satisfied in the implementation.

For each security guardrail in the ACF:
- Guardrail (from ACF §3):
- How verified (code review, test, scan, manual check):
- Evidence:
- Status: Verified | Not Verified | N/A

If ACF defines security review triggers and any were matched during execution, confirm that security review was performed:
- Trigger matched:
- Review performed: Yes | No
- Reviewer:
- Outcome:

## 8. Runbook Verification
Verify that operational procedures from TDD §9 (Operational Notes) are documented and tested.

- [ ] Deploy procedure documented and tested
- [ ] Verify procedure documented and tested
- [ ] Rollback procedure documented and tested
- [ ] Ownership/on-call expectations documented

Evidence:

## 9. Open Items
List anything not yet verified. Each item must have an owner and a deadline.

| Item | Owner | Deadline | Blocks Production? |
|------|-------|----------|-------------------|
|      |       |          | Yes / No          |

## 10. Readiness Declaration (when ready)
This system is operationally ready for production.

- Approved By:
- Date:
