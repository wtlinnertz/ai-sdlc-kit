# ACF — Standard Service Guardrails

## 0. Document Control
- ACF ID: ACF-EX-001
- Owner: Platform Team (Example)
- Date: 2025-01-10
- Status: Frozen
- Applies To: All internal services

## 1. Purpose
Define architectural guardrails that constrain the design of internal services deployed on the standard platform. These guardrails ensure consistency, security, and operability.

## 2. Platform Assumptions (High Level)
- Runtime environment(s): Managed container runtime
- Deployment model(s): Standard CI/CD pipeline with GitOps promotion
- Networking posture: Internal network only; no public ingress by default
- Identity model: Service-to-service authentication via platform identity provider

## 3. Security Guardrails (Hard)
- Authentication: Service-to-service authentication required for all API calls
- Authorization: Consumers must present valid service credentials
- Data classification: Internal use only; no PII in reference data
- Encryption: TLS required for all in-transit communication
- Secrets handling: Secrets must be injected via platform secrets manager; no hardcoded secrets

### Security Review Triggers
A dedicated security review is required during execution when any of the following occur:
- Changes to service-to-service authentication or authorization logic
- Introduction of new API endpoints accessible by external consumers
- Changes to secrets handling or injection mechanisms
- New external dependencies added to the service
- Changes to data classification or handling of sensitive data

When triggered, the review phase must include security-specific verification against the guardrails in this section.

## 4. Compliance / Regulatory Constraints (Hard)
- All services must produce audit-ready logs
- No data may leave the internal network boundary

## 5. Reliability & Resilience Guardrails (Hard)
- Availability: Service must be available during business hours
- Failure isolation: Failures must not propagate to consumers (fail gracefully)
- Rollback: All deployments must support rollback to the previous version

## 6. Observability Guardrails (Hard)
- Required telemetry: Structured logs, request metrics, health check endpoint
- Minimum operational signals: Request count, error rate, latency percentiles

## 7. Approved Architectural Patterns
- Request/response over HTTP
- Stateless service design
- Read-through from a backing data store

## 8. Forbidden Patterns (Hard)
- Direct database access by consumers (must go through the API)
- Shared mutable state between service instances
- Synchronous calls to external systems during request handling

## 9. Standard Interfaces / Integrations (Optional)
- Change management: Standard change request process
- CI/CD: Standard pipeline with automated build, test, deploy stages
- Artifact storage: Container images stored in organization registry
- Audit: Structured logs forwarded to central log aggregator

## 10. Open Items
- None

## 11. Freeze Declaration
This ACF is approved and frozen. SAD and downstream artifacts must comply.

- Approved By: Platform Team (Example)
- Date: 2025-01-10
