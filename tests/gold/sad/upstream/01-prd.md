# PRD — Reference Data Service

## 0. Document Control
- PRD ID: PRD-EX-001
- Author: Example Team
- Date: 2025-01-15
- Status: Frozen
- Related Links: None

## 1. Problem Statement
Multiple internal service teams require access to the same reference data.
Today, each consuming system embeds its own copy, leading to inconsistency and duplication.
This creates maintenance overhead for service teams and risks data drift across consumers.

A recent audit identified three incidents caused by stale reference data in the past quarter.
Consolidation is needed now because the number of consuming systems is growing, and each new consumer increases the cost and risk of the current approach.

## 2. Goals (What "Success" Means)
- Provide a single authoritative source for reference data, measured by all consuming systems retrieving data from the new service instead of local copies
- Reduce duplication across consuming systems, measured by the removal of embedded reference data from at least two existing systems within 90 days of launch

## 3. Non-Goals (Hard Exclusions)
- No UI or human-facing interface
- No write or mutation capability
- No external exposure outside the internal network

## 4. Users / Personas
- Internal service consumers (automated systems retrieving reference data)
- Automated batch processes (scheduled jobs that read reference data)

## 5. Requirements

### 5.1 Functional
- FR-1: The system SHALL expose an API to retrieve reference data by key
- FR-2: The system SHALL return data in a consistent schema
- FR-3: The system SHALL return an appropriate error when a key is not found

### 5.2 Non-Functional
- NFR-1: The system SHALL respond to API requests within 200ms at the 95th percentile under normal load
- NFR-2: The system SHALL be available during business hours (Monday–Friday, 08:00–18:00 local time, 99.5% uptime target)
- NFR-3: The system SHALL produce structured logs for all requests

## 6. Constraints (Hard Guardrails)
- Must run on the standard platform runtime
- Must follow organization security baseline
- Must use service-to-service authentication

## 7. Assumptions
- Reference data volume is modest (thousands of records, not millions). If false, data storage and query strategy may need to change.
- Consumers can tolerate eventual consistency. If false, real-time synchronization would be required, significantly expanding scope and architecture.
- Reference data is updated infrequently (hours or days, not seconds). If false, a change-event or streaming model would be needed instead of a simple read API.

## 8. Out of Scope by Default
Anything not listed in Sections 2 and 5 is out of scope, including:
- Data ingestion pipelines
- Administrative tooling
- Caching layers beyond what the platform provides

## 9. Open Questions
- None

## 10. Acceptance / Success Criteria
- At least two consuming systems migrate to the new service within 90 days of launch
- Duplicate reference data implementations are removed from migrated systems
- Service passes all validator and readiness gates
- Zero incidents caused by stale reference data in migrated systems over a 30-day post-launch window

## 11. Freeze Declaration
This PRD is approved and frozen. Architecture work may proceed.

- Approved By: Example Team
- Date: 2025-01-15
