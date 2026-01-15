# TDD — Reference Data Service

## Intent Summary
(Approved intent summary applies)

## Scope
- Implement read-only API
- Integrate with reference data store

## Non-Goals
- Write operations
- UI

## Interfaces
- GET /reference-data/{key}

## Build and Deployment
- Build container image
- Deploy via standard pipeline

## Failure Handling
- Return error when data unavailable
- Roll back on failed deployment

## Testing Strategy
- Unit tests for data access
- Integration test for API

## Freeze Declaration
Approved and frozen.
