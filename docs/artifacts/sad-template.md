# SAD Template (System Architecture Design)

## 0. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | SAD-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| System Name | |
| Author | |
| Date | |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

- Upstream Artifacts:
  - PRD ID / Link:
  - ACF ID / Link:
- Related ADRs:

## 1. Intent Summary
Restate the upstream intent, constraints, and non-goals from the PRD in 8–12 bullets.
Do not add requirements or design. Do not expand scope.

## 2. Scope and Non-Goals (Hard Boundary)

### In Scope
- Item 1:
- Item 2:

### Explicit Non-Goals
- Non-goal 1:
- Non-goal 2:

## 3. System Context (Black Box)
Describe the system as a black box.

### Responsibilities
- Responsibility 1:
- Responsibility 2:

### External Actors / Systems
- Upstream:
- Downstream:
- Users/Clients:

### Trust Boundaries
- Boundary 1:
- Boundary 2:

### Diagrams
Include a C4 Context (L1) diagram in Mermaid showing the system and its external actors.

```mermaid
graph TB
    %% C4 Context diagram here
```

## 4. High-Level Architecture (White Box)
Define major components and interactions.

### Major Components
For each component:
- Name:
- Responsibility:
- Key interactions:

### Layer Assignment

**Dependency Direction Rule:** Source code dependencies point inward only. Infrastructure → Application → Domain. Domain depends on nothing external.

| Component | Layer | Justification |
|-----------|-------|---------------|
| {component name} | Domain / Application / Infrastructure | {why this layer} |

Components that span layers (if any):
- {component}: {which layers and why}

### Communication Patterns
- Sync vs async:
- Protocols (high level):
- High-level data flow:

### Diagrams
Include a C4 Container (L2) diagram and a Data Flow diagram in Mermaid.

```mermaid
graph LR
    %% C4 Container diagram here
```

```mermaid
graph LR
    %% Data Flow diagram here
```

## 5. Key Architectural Decisions
Record only decisions that affect system shape.
Each decision should reference an ADR when applicable.

- Decision:
  - Rationale:
  - Alternatives considered:
  - Consequences:

## 6. Cross-Cutting Concerns (Architectural Handling)

### Security
- Authn/authz posture:
- Data protection posture:

### Reliability and Resilience
- Failure isolation strategy:
- Retry/fallback philosophy:

### Observability
- What must be observable (not how):

### Performance and Scale
- Scaling model (high level):
- Constraints (high level):

## 7. Data and Integration

### Data Stores
For each data store:
- Name:
- Ownership:
- Access pattern:

### Integration Patterns
- Pattern 1:
- Pattern 2:

### Integration Contracts

For each cross-service integration point (boundaries where independently deployed services communicate):

| Integration Point | Service A | Service B | Expected Inputs | Expected Outputs | Error Modes | Versioning Strategy |
|-------------------|-----------|-----------|----------------|-----------------|-------------|-------------------|
| {name} | {service} | {service} | {format, schema, required fields} | {format, schema, response codes} | {timeout, unavailable, malformed input} | {URL versioning, header versioning, backward-compatible} |

*Internal component interactions within a single service are exempt from this table.*

### State Transitions
Describe data or artifact state transitions at the architectural level.

## 8. Failure Modes and Recovery

| Failure Mode | Impact | Detection | Mitigation |
|-------------|--------|-----------|------------|
| Mode 1 | | | |
| Mode 2 | | | |

## 9. Quality Attribute Scenarios (QAS)

Define at least one scenario per major quality attribute.

| Quality Attribute | Scenario | Response | Measure |
|------------------|----------|----------|---------|
| Availability | | | |
| Performance | | | |
| Security | | | |

## 10. Constraints and Guardrails (from ACF)
List hard constraints that downstream artifacts must respect.
- Guardrail 1:
- Guardrail 2:

## 11. Deferred Decisions (Explicit)
List items intentionally deferred to TDD-level detail.
- Deferred 1:
- Deferred 2:

## 12. Risks and Assumptions

### Risks
- Risk 1:
- Risk 2:

### Assumptions
- Assumption 1:
- Assumption 2:

## 13. Freeze Declaration (when ready)
This SAD is approved and frozen. Downstream artifacts may not reinterpret or expand this architecture.

- Approved By:
- Date:
