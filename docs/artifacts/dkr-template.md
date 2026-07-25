# DKR Template (Domain Knowledge Record)

The DKR defines the **domain model** — concepts, relationships, rules, language, and workflows — as a reusable, freezable artifact.
It is architecture-agnostic and constrains SAD and TDD creation.

## 1. Document Control

| Field | Value |
|-------|-------|
| Artifact ID | DKR-{PROJECT}-{NNN} |
| Owner | {owner} |
| Status | DRAFT |
| Initiative/Scope | |
| Date | |
| Applicability Scope | (e.g., "All initiatives in the CI/CD domain", "Payment processing services") |
| Version | |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

## 2. Ubiquitous Language

| Term | Definition | Synonyms to Avoid | Used In |
|------|------------|--------------------|---------|
| {Term 1} | {Precise, unambiguous definition} | {Synonyms that cause confusion} | §3, §5 |
| {Term 2} | | | |
| {Term 3} | | | |
| {Term 4} | | | |
| {Term 5} | | | |

Minimum 5 terms required. Add rows as needed.

## 3. Domain Entities

| Entity | Description | Key Attributes | Lifecycle States |
|--------|-------------|----------------|------------------|
| {Entity 1} | {What this concept IS in the domain} | {Domain-level attributes} | {Domain states, if applicable} |
| {Entity 2} | | | |

Every entity referenced in §4–§6 must be defined here. Attributes must be domain-level, not implementation-level. Lifecycle states must be domain states, not system states.

## 4. Entity Relationships

| From Entity | Relationship Type | To Entity | Cardinality | Description |
|-------------|-------------------|-----------|-------------|-------------|
| {Entity A} | owns / references / triggers / produces / consumes / depends-on | {Entity B} | 1:1 / 1:N / N:M | {Why this relationship exists} |
| | | | | |

Every entity in §3 with connections must appear here. Relationship type must be explicit. Cardinality must be stated.

## 5. Domain Rules

### DR-001: {Rule Name}
- **Rule Statement:** {Specific enough to validate in a test scenario}
- **Entities Involved:** {List entities from §3}
- **Enforcement Point:** {Where in the lifecycle this rule applies}

### DR-002: {Rule Name}
- **Rule Statement:**
- **Entities Involved:**
- **Enforcement Point:**

Add rules as needed. No aspirational language. Each rule must reference at least one entity from §3.

## 6. Workflows

### Workflow 1: {Name}
- **Trigger:** {What initiates this workflow}
- **Steps:**
  1. {Domain action referencing entities from §3}
  2. {Domain action — no tool names, no commands}
  3. {Domain action referencing rules from §5 where applicable}
- **Outcome:** {What state the domain is in when this workflow completes}

### Workflow 2: {Name}
- **Trigger:**
- **Steps:**
  1.
  2.
- **Outcome:**

Add workflows as needed. Describe WHAT happens in domain terms, not HOW.

## 7. Bounded Contexts

### In Scope
- {What this domain model covers}
- {Boundary statement}

### Out of Scope
- {What this domain model explicitly does NOT cover}
- {Adjacent concerns that belong to other domains}

### Adjacent Domain Interfaces

| Domain | Interface | Interaction Type | Notes |
|--------|-----------|------------------|-------|
| {Adjacent domain} | {What is exchanged} | shared kernel / customer-supplier / conformist / anticorruption layer / separate ways | {Additional context} |
| | | | |
