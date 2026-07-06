# ACF Template (Architecture Context File)

The ACF defines **architecture guardrails** that constrain the SAD and downstream artifacts.
It is reusable across many initiatives.

## 0. Document Control
- ACF ID:
- Owner:
- Date:
- Status: Draft | Approved | Freeze Pending | Frozen
- Governance Model Version: 1.0
- Prompt Version: {prompt version}
- Spec Version: {spec version}
- Principles Version: {principles file versions}
- Applies To: (e.g., “All services”, “All platform workloads”, “This domain only”)

## 1. Purpose
What guardrails does this ACF exist to enforce?

## 2. Platform Assumptions (High Level)
- Runtime environment(s):
- Deployment model(s):
- Networking posture (high level):
- Identity model (high level):

## 2a. Platform Context
[ ] PINFK adopted — PDR IDs: \_\_\_, ISPEC ID:\_\_\_ | [ ] PINFK not adopted — platform assumptions: \_\_\_

## 3. Security Guardrails (Hard)
Examples (customize to your organization’s baseline):
- Authentication requirements:
- Authorization expectations:
- Data classification and handling:
- Encryption requirements (in transit / at rest):
- Secrets handling expectations:

### Security Review Triggers
Define conditions under which a dedicated security review is required during execution:
- Trigger 1: (e.g., changes to authentication or authorization flows)
- Trigger 2: (e.g., handling of sensitive data — PII, PHI, PCI)
- Trigger 3: (e.g., new externally-facing API endpoints)
- Trigger 4: (e.g., changes to cryptographic implementations)
- Trigger 5: (e.g., new external dependencies)

When triggered, the review phase must include security-specific verification against the guardrails in this section.

## 4. Compliance / Regulatory Constraints (Hard)
- Constraint 1:
- Constraint 2:
- Data retention / archival requirements:

## 5. Reliability & Resilience Guardrails (Hard)
- Availability expectations (qualitative):
- Failure isolation expectations:
- Rollback expectations:
- Disaster recovery expectations:

## 6. Observability Guardrails (Hard)
- Required telemetry types: logs, metrics, traces (as applicable)
- Minimum operational signals required:

## 7. Approved Architectural Patterns
List “allowed” patterns that are preferred or standard.
- Pattern 1:
- Pattern 2:

## 8. Forbidden Patterns (Hard)
List explicitly prohibited approaches.
- Forbidden 1:
- Forbidden 2:

## 9. Standard Interfaces / Integrations (Optional)
- Change management expectations:
- CI/CD expectations:
- Artifact storage expectations:
- Audit expectations:

## 10. Open Items
- Open item 1:
- Open item 2:

## 11. Freeze Declaration (when ready)
This ACF is approved and frozen. SAD and downstream artifacts must comply.

- Approved By:
- Date:
