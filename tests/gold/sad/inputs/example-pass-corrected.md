# SAD — Reference Data Service

## 0. Document Control
- System Name: Reference Data Service
- SAD ID: SAD-EX-001
- Author: Example Team
- Date: 2025-01-20
- Status: Frozen
- Upstream Artifacts:
  - PRD: PRD-EX-001
  - ACF: ACF-EX-001
- Related ADRs: None

## 1. Intent Summary
(Restated from PRD-EX-001)

- Provide read-only access to reference data via a single internal API
- Serve internal service consumers and automated batch processes only
- No UI, no data mutation, no external exposure
- Must follow standard platform guardrails (ACF-EX-001)
- Architecture should be simple: stateless API backed by a data store
- Must support rollback, structured logging, and health checks
- Reference data volume is modest; eventual consistency is acceptable
- Service-to-service authentication required for all consumers

## 2. Scope and Non-Goals (Hard Boundary)

### In Scope
- Read-only API for retrieving reference data by key
- Internal consumption only
- Structured logging and health check endpoint
- Service-to-service authentication

### Explicit Non-Goals
- Data mutation or write operations
- User interface of any kind
- External network exposure
- Data ingestion or pipeline management
- Caching beyond platform defaults

## 3. System Context (Black Box)

### Responsibilities
The Reference Data Service is responsible for serving reference data to internal consumers via a read-only API.

### External Actors / Systems
- Internal service consumers: Send authenticated GET requests to retrieve reference data
- Automated batch processes: Query reference data on a scheduled basis
- Platform identity provider: Validates service credentials
- Central log aggregator: Receives structured logs

### Trust Boundaries
- All inbound traffic is internal-only (no public ingress)
- All consumers must present valid service credentials
- The service trusts the platform identity provider for authentication

### Diagrams

```mermaid
graph TB
    C1[Service Consumer A] -->|"Sync HTTP GET"| RDS
    C2[Service Consumer B] -->|"Sync HTTP GET"| RDS
    C3[Batch Process] -->|"Sync HTTP GET"| RDS
    IDP[Identity Provider] -.->|"Sync auth validation"| RDS

    subgraph System Boundary
        RDS[Reference Data Service]
    end

    RDS -->|"Sync read"| DS[(Data Store)]
    RDS -->|"Async log forwarding"| LA[Log Aggregator]
```

## 4. High-Level Architecture (White Box)

### Major Components
- **API Component**: Handles HTTP requests, authentication validation, request routing, and error responses
- **Data Access Component**: Reads from the backing data store, maps data to the response schema

### Layer Assignment

Dependency direction rule: dependencies point inward only (Infrastructure -> Application -> Domain). No domain component may depend on an infrastructure component.

| Component | Layer |
|-----------|-------|
| Reference data lookup rules (key validation, response shaping) | Domain |
| API Component (request handling, routing, auth enforcement) | Application |
| Data Access Component (data store client) | Infrastructure |
| Structured logging emitter | Infrastructure |

### Communication Patterns
- Synchronous request/response over HTTP between consumers and API
- Synchronous read from data store by data access component
- Asynchronous log forwarding to central aggregator

### Diagrams

```mermaid
graph LR
    subgraph Reference Data Service
        API[API Component] --> DAC[Data Access Component]
    end
    DAC --> DS[(Data Store)]
    API --> LOG[Structured Logging]
```

```mermaid
graph LR
    Consumer -->|HTTP GET| API[API Component]
    API -->|Query| DAC[Data Access Component]
    DAC -->|Read| DS[(Data Store)]
    DS -->|Result| DAC
    DAC -->|Response DTO| API
    API -->|JSON Response| Consumer
```

## 5. Key Architectural Decisions

| Decision | Rationale | ADR |
|----------|-----------|-----|
| Use synchronous request/response model | Simplest pattern for read-only lookups; aligns with approved patterns in ACF-EX-001 | N/A |
| Centralize data access behind API | Prevents direct database access by consumers; enforces forbidden pattern from ACF-EX-001 | N/A |
| Stateless service design | Enables simple rollback and horizontal scaling if needed | N/A |

## 6. Cross-Cutting Concerns (Architectural Handling)

### Security
- Service-to-service authentication enforced at the API component level
- TLS required for all communication (per ACF-EX-001)
- No secrets stored in application code; injected via platform secrets manager

### Reliability / Resilience
- Service is stateless; any instance can serve any request
- Failed deployments are rolled back to the previous container image
- Data store unavailability returns a clear error response; does not crash the service

### Observability
- Structured JSON logs emitted for every request (method, path, status, latency)
- Health check endpoint at `/health`
- Request count, error rate, and latency percentiles exposed as metrics

### Performance / Scale
- Reference data volume is modest; no caching layer required
- Stateless design allows horizontal scaling if demand increases
- Single data store read per request; no fan-out

## 7. Data and Integration

### Data Stores
- **Reference Data Store**: Owned by the Reference Data Service (authoritative source of truth for reference data within this system). This service has read-only access. Write access is held exclusively by an external data loading process outside this service's boundary; no component within this service has write access.

### Integration Patterns
- Consumers integrate via synchronous HTTP GET requests
- No event-driven or messaging integration; all interactions are request/response

### Integration Contracts

The consumer-to-service boundary is the only point where independently deployed services communicate. Its contract:

| Aspect | Contract |
|--------|----------|
| Expected inputs | Authenticated HTTP GET `/reference/{key}`; `key` is a URL-safe string; service credential in the `Authorization` header |
| Expected outputs | `200` with a JSON body `{"key": string, "value": object, "as_of": timestamp}`; `404` when the key does not exist |
| Error modes | `401` unauthenticated; `403` credential lacks read scope; `503` with `Retry-After` when the data store is unavailable |
| Versioning strategy | URI version prefix (`/v1/`); breaking changes require a new major prefix and a deprecation window for the old one |

All other interactions (API Component to Data Access Component, logging emitter) are internal component interactions and carry no cross-service contract requirement.

### State Transitions
- Reference data is static from this service's perspective; no state transitions occur within the service boundary
- Data freshness is managed by the external data loading process (out of scope)

## 8. Failure Modes and Recovery

| Failure Mode | Impact | Detection | Mitigation |
|-------------|--------|-----------|------------|
| Data store unavailable | Consumers receive error responses | Health check fails; error rate metric spikes | Service returns graceful error; stateless design allows restart without data loss |
| Identity provider unavailable | Authentication fails; all requests rejected | Auth failure rate metric spikes | Service returns 503; consumers retry with backoff |
| Reference data stale or missing | Consumers receive outdated or empty results | Monitoring on data freshness (external) | Out of scope — data loading is managed externally |

## 9. Quality Attribute Scenarios (QAS)

| Quality Attribute | Scenario | Response | Measure |
|------------------|----------|----------|---------|
| Availability | Data store becomes unreachable during normal operation | Service returns structured error response; does not crash; recovers when store is available | Service remains responsive; error rate visible in metrics |
| Performance | Consumer sends a lookup request for a single key | Service reads from data store and returns JSON response | Response within acceptable latency for internal service calls |
| Security | Unauthenticated request arrives at the API | Service rejects the request with 401; no data is returned | Zero unauthorized data access |

## 10. Constraints and Guardrails (from ACF)
- ACF-EX-001 constraints apply in full
- No public ingress
- Service-to-service authentication required
- Rollback must be supported
- Direct database access by consumers is forbidden
- Structured logs and health check are mandatory

## 11. Deferred Decisions (Explicit)

| Decision | Reason | Target Resolution Phase |
|----------|--------|------------------------|
| Storage technology selection | Not an architectural concern; any read-capable store suffices | TDD |
| Specific metrics tooling | Platform-dependent; not an architectural constraint | TDD |

## 12. Risks and Assumptions

| Risk | Impact | Mitigation |
|------|--------|------------|
| Data store becomes unavailable | Consumers receive errors | Service returns graceful error; consumers expected to handle failures |
| Reference data grows beyond modest volume | Latency increases | Stateless design supports scaling; caching can be added as a future enhancement |

### Assumptions
- Reference data volume remains modest for the foreseeable future
- Platform identity provider is reliable and available
- Central log aggregator is operational

## 13. Readiness Checklist (Self-Check)
- [x] Intent summary matches PRD
- [x] Non-goals are explicit
- [x] ACF guardrails are addressed
- [x] System boundary is clear
- [x] Major components are identified
- [x] C4 Context (L1) diagram present
- [x] C4 Container (L2) diagram present
- [x] Data Flow diagram present
- [x] Data stores and integrations documented
- [x] Failure modes table complete
- [x] At least one QAS per quality attribute
- [x] Architectural decisions are documented
- [x] Deferred decisions are explicit
- [x] No implementation details present

## 14. Freeze Declaration
This SAD is approved and frozen. TDD work may proceed.

- Approved By: Example Team
- Date: 2025-01-20
