# How to Adapt aieos-engineering-execution to Your Organization

This guide explains **what you should customize**, **what must remain invariant**, and **how to layer organizational policy** on top of aieos-engineering-execution without breaking its guarantees.

The goal is adoption without dilution.

## First: what this kit is (and is not)

aieos-engineering-execution is:
- A **process and artifact model**
- A **set of enforceable quality gates**
- A **safe way to use AI across the SDLC**

aieos-engineering-execution is not:
- A toolchain
- A framework
- A prescriptive architecture
- A replacement for engineering judgment

You are expected to adapt it carefully.

## Invariants (Do Not Change These)

The following concepts must remain intact if you want the system to work as designed.

### 1. Artifact promotion model
- Artifacts are promoted, not rewritten.
- Each artifact has a single responsibility.
- Downstream artifacts may not expand scope.

If this breaks, rework and ambiguity return immediately.

### 2. Freeze points
- PRD, SAD, TDD, and WDD must have explicit freeze moments.
- Promotion without freeze undermines traceability.

You may automate freezes, but you may not remove them.

### 3. Validators as hard gates
- Validators decide readiness.
- Ambiguity is a failure condition.
- Validators do not redesign or suggest solutions.

Soft validators turn this into documentation theater.

### 4. Non-goals are enforceable
- Non-goals must be explicit.
- Validators must block violations.
- “Helpful” scope expansion is not allowed.

This is the most common failure mode in adoption.

### 5. Granularity rules for execution
- One outcome.
- One repo/subsystem.
- One PR.
- One environment.

If you relax granularity, AI effectiveness drops sharply.

## What You SHOULD Customize

These are the **intended extension points**.

### 1. Architecture context files (ACFs)

ACFs are the primary place to encode:
- Security requirements
- Compliance constraints
- Platform standards
- Forbidden patterns
- Approved integrations

You will almost certainly need:
- One global ACF
- Optional domain- or platform-specific ACFs

ACFs let you adapt without changing templates or validators.

---

### 2. Design context files (DCFs)

DCFs define:
- Design principles
- Quality bars
- Testing expectations
- Operational standards

Use DCFs to:
- Encode engineering standards
- Set quality expectations
- Align multiple teams

Do not hardcode these into templates.

### 3. Validator integration points

You may:
- Integrate validators into CI
- Use them in internal portals
- Enforce them via workflow transitions
- Run them manually during reviews

You may also:
- Add **organization-specific gates**
- Add **additional validators**

Do not weaken existing gates without understanding the trade-offs.

### 4. Work system field mapping

You will need to adapt:
- Field names
- Labels
- Custom fields
- Workflow states

This does **not** require changing:
- WDD work item structure
- DoR logic
- Granularity rules

Map the model to your tooling, not the other way around.

### 5. Enforcement strictness (carefully)

You may choose:
- Where enforcement is automated
- Where humans approve
- Where exceptions are allowed

If you allow exceptions:
- Make them explicit
- Make them visible
- Make them rare

Invisible exceptions rot the system.

## What you should avoid customizing early

These changes usually cause more harm than good.

### ❌ Combining Artifacts
Example: “Let’s merge SAD and TDD.”

This removes clarity and makes validation harder.

### ❌ Making Validators Helpful
Example: “Let’s have the validator suggest improvements.”

This causes silent redesign and scope creep.

### ❌ Overloading Templates
Example: Adding org-specific fields everywhere.

Use ACFs and DCFs instead.

### ❌ Removing Intent Verification from Prompts
Intent verification is the cheapest alignment step in the system.

Removing it from prompts costs more later. Validators catch misalignment, but only after a full generation cycle.

## Setting up your project

### Where the kit lives

Keep the kit as a central, shared repository. Teams reference the kit's prompts, validators, and templates—they do not copy them into each project. When the kit improves, every team benefits immediately.

### Where artifacts live

Generated artifacts (PRD, SAD, TDD, WDD, ORD) live in the **app repo** under a conventional path:

```
my-app/
  docs/sdlc/
    01-prd.md
    02-sad.md
    03-tdd.md
    04-wdd.md
    05-ord.md
```

The numbered prefix follows the artifact flow, so the directory listing reads in promotion order.

**Why the app repo?** Artifacts describe *this* system. They should live with it. git gives you version history, branching, and freeze semantics for free. prd changes and code changes share the same history, making traceability natural.

### Where ACF and DCF live

This depends on your organization:

**If your organization has shared standards**. ACF and DCF live in a central location (the kit repo, a governance repo, or wherever org-level standards are maintained). Projects reference them; they are not duplicated per project.

**If teams set their own standards**. ACF and DCF are project-level artifacts and live in `docs/sdlc/` alongside everything else:

```
my-app/
  docs/sdlc/
    01-prd.md
    02-acf.md
    03-sad.md
    04-dcf.md
    05-tdd.md
    06-wdd.md
    07-ord.md
```

**If some standards are shared and some are team-specific**. Use an org-level ACF/DCF for the shared baseline. Teams can extend with a project-level ACF/DCF that adds team-specific constraints without contradicting the org-level file. Reference both as inputs when generating artifacts.

Start with project-level context files. Extract to a shared location only when you've proven reuse across multiple projects.

### Where human-authored inputs live

Some artifacts require human-authored inputs before they can be generated:

- **Product Brief**: feeds the PRD prompt (template: `product-brief-template.md`)
- **Architecture Context**: feeds the ACF prompt (template: `architecture-context-template.md`)
- **Design Context**: feeds the DCF prompt (template: `design-context-template.md`)
- **System Context**: feeds the SAD prompt for brownfield projects (template: `system-context-template.md`)

These are not AI-generated artifacts: they are the human decisions that drive generation. For brownfield projects, the `codebase-analysis-prompt.md` can pre-fill the Architecture Context, Design Context, and System Context forms from codebase analysis: the human reviews and edits before using them as input.

Store intake forms in `docs/sdlc/` with a `00-` prefix to distinguish them from generated artifacts:

```
my-app/
  docs/sdlc/
    00-product-brief.md          ← human input
    00-architecture-context.md   ← human input
    00-design-context.md         ← human input (optional, for DCF)
    00-system-context.md         ← human input (brownfield only, for SAD)
    01-prd.md                    ← generated, validated, frozen
    02-acf.md
    ...
```

The `00-` prefix keeps inputs visually grouped before the generated artifacts in directory listings.

### Configuring AI tool awareness

Most AI tools support project-level instruction files that are loaded at the start of every session. Use these to give the AI automatic awareness of the kit and your project's conventions. Without manually pasting instructions each time.

See `how-to-use-with-ai.md` → "Setting Up Your AI Tool" for the specific file names per tool and what to include.

At minimum, the instruction file should reference:
- The kit's location (path to prompts, specs, templates, validators)
- Your project's artifact directory (`docs/sdlc/`)
- The artifact flow and key constraints (freeze-before-promote, separate sessions)

This is especially important when the kit is a shared repository separate from the project repo. The ai needs to know where to find both.

### Where validator results live

Store the final passing validator result alongside the artifact it validated:

```
my-app/
  docs/sdlc/
    01-prd.md
    01-prd-validation.json
    02-acf.md
    02-acf-validation.json
    ...
```

The pattern is `{nn}-{type}-validation.json`. Store only the final passing result: the one that gates the freeze decision. Earlier failed attempts are in git history if needed.

## Proportional use: when to abbreviate the artifact chain

The full EEK chain (Kit Entry → PRD → ACF → SAD → DCF → TDD → WDD → execution → ORD) is appropriate for significant features and system changes. For smaller, well-understood work, some artifacts can be abbreviated or shared from prior engagements without weakening the system's guarantees.

The rule is: **the scope of governance should match the scope of the decision.** A 1-day bug fix does not need a new SAD. A well-understood enhancement does not need a new TDD from scratch if the TDD from the prior engagement covers the same system boundaries.

### Artifact scope by work type

| Work Type | Kit Entry | PRD | ACF | SAD | DCF | TDD | WDD | ORD |
|-----------|-----------|-----|-----|-----|-----|-----|-----|-----|
| New feature / initiative | Required | Required | Required | Required | Required | Required | Required | Required |
| Enhancement to existing feature | Required | Required | Reuse existing | Reuse existing | Reuse existing | Required (new scope) | Required | Required |
| Tech debt / refactor | Required | Required | Reuse existing | Conditional* | Reuse existing | Conditional* | Required | Conditional** |
| Bug fix (clear repro, no design) | Required | Abbreviated† | Reuse existing | Not required | Reuse existing | Not required | Required | Conditional** |
| Compliance mandate (externally specified) | Required | Required | Reuse/update | Conditional* | Reuse existing | Conditional* | Required | Required |

**Legend:**
- **Reuse existing**: Use the frozen artifact from the most recent relevant engagement. If the system boundary it covers has not changed, regeneration is not required.
- **Conditional***: Required if the work changes system architecture or technical interfaces, not required if it is contained within an existing component boundary.
- **Conditional**: Required if the work changes deployment, observability, or operational characteristics, not required if the fix is self-contained and the existing ORD evidence base still holds.
- **Abbreviated†**: For bug fixes, the PRD may be abbreviated to: Problem Statement (what breaks, who is affected, why now), Non-Goals (what the fix does not change), and Acceptance Criteria (what passing looks like). Sections not applicable to a bug fix may be marked "N/A (bug fix)" with a one-line explanation.

### Rules for reuse

Reusing a frozen artifact from a prior engagement is valid only if:
1. The artifact is still frozen (has not been modified since its validation PASS)
2. The system or domain it covers has not changed in ways that would affect the current work
3. The human team confirms reuse is appropriate (a human decision, not an AI inference)

If there is any doubt, regenerate. Generating from an outdated context produces worse artifacts than regenerating from scratch.

### What never changes

Regardless of work type or scope:
- **Kit Entry Gate (Step 0) always applies**: classification, path selection, priority, scope boundary
- **Validators always apply**: whatever artifacts are produced must pass their validators
- **Freeze always applies**: artifacts that are used must be frozen
- **Human approval always applies** at each freeze point

Proportional governance means doing less paperwork for smaller work. It does not mean skipping the quality bar for the work you do.

## Recommended adoption path

A proven, low-risk path:

1. Use the kit **as-is** on one pilot initiative
2. Set up `docs/sdlc/` in your app repo
3. Add a **minimal ACF** (project-level is fine to start)
4. Add a **minimal DCF** (project-level is fine to start)
5. Integrate the **DoR validator** first
6. Expand enforcement gradually
7. Extract ACF/DCF to a shared location only after reuse is proven
8. Only then customize further

Do not start by changing templates or validators.

## Scaling across teams

When scaling:
- Extract proven ACFs and DCFs to a shared location
- Assign ownership for shared context files
- Version ACFs and DCFs, treat changes as breaking or non-breaking
- Communicate changes explicitly
- Allow team-level extensions that add constraints without contradicting shared standards

The model scales best when **context is centralized** and **execution is decentralized**.

## Using complexity estimates for planning

WDD work items include a **Complexity Estimate** (S, M, or L) and a **Required Capabilities** list. These are planning signals, not commitments.

### What the AI provides

The AI assigns complexity based on **structural factors visible in the WDD**:

| Factor | What It Measures |
|--------|-----------------|
| Scope indicator count | Number of In Scope bullets |
| Acceptance criteria count | Testing surface (including failure conditions) |
| Dependency count | Coordination overhead with other work items |
| Capability breadth | Number of distinct skill domains required |
| Integration surface | Whether external systems or boundaries are involved |
| Novelty | Whether patterns are well-established or unfamiliar |

Each estimate includes a one-sentence justification referencing these factors, so the reasoning is transparent and auditable.

### What the AI cannot know

The AI has no knowledge of:
- Your team's velocity or historical throughput
- Individual team members' skill levels or availability
- The current state of the codebase (tech debt, test coverage, documentation quality)
- Your organization's ceremony overhead (PR review turnaround, deployment windows, approval chains)
- Whether "backend" work in your codebase is straightforward or involves a legacy system

**This is why complexity estimates are advisory, not hard gates.**

### Calibrating S/M/L to your team

Each team should establish their own calibration table that maps S/M/L to effort ranges based on actual velocity data. Example:

| Size | Typical Effort (Team A) | Typical Effort (Team B) |
|------|------------------------|------------------------|
| S | 2–4 hours | Half day |
| M | 1–2 days | 1–3 days |
| L | 3–5 days | 3–7 days |

To build this calibration:
1. Run the kit on 2–3 initiatives without calibrating
2. Record actual effort per work item alongside the AI's S/M/L estimate
3. After 15–20 completed work items, calculate your team's average effort per size
4. Use that as your planning baseline. Update quarterly as the team evolves

### How POs and PDMs should use this

**For sprint planning:**
- Use Required Capabilities to identify *who* can do the work
- Use Complexity Estimate to estimate *how much* work it is (after calibration)
- Use Dependencies to determine *ordering* constraints
- Use Work Groups to identify *what can be parallelized*

**For capacity planning:**
- Sum the calibrated effort per size across work items
- Compare against available team capacity per capability domain
- Identify bottlenecks where too many items require the same capability

**What to watch for:**
- If the AI consistently over- or under-estimates relative to your team's experience, adjust your calibration, don't change the AI's sizing factors
- If most items are sized L, the WDD may need further decomposition (granularity rules may not be strict enough)
- If all items are sized S, the TDD scope may be too small for structured governance overhead

## Parallel development with interface contracts

One of the most practical benefits of the TDD's **§4 Interfaces and Contracts** section is enabling developers to work in parallel across component boundaries. A frontend developer and a middleware developer, or a middleware developer and a database developer, coding simultaneously against an agreed contract.

### How it works

The artifact flow naturally produces the contracts needed for parallel work:

1. **SAD** defines the components, boundaries, and interaction types (sync API, async event, etc.)
2. **TDD §4** specifies the exact contracts: inputs, outputs, schemas, error modes, backward compatibility
3. **WDD** decomposes work so that each item references the specific TDD contract it implements or consumes
4. **Developers** implement their side of the contract independently, using stubs or mocks for the other side

The TDD contract is the agreement. Once frozen, both sides code against it without waiting for each other.

### Contract-first development pattern

After the TDD is frozen, teams can follow this pattern:

1. **Extract contracts**. Identify every interface in TDD §4 that crosses a component boundary
2. **Assign sides**. Each side of the contract belongs to a different work item (and potentially a different developer)
3. **Build stubs first**. Each developer creates a stub or mock of the *other* side from the TDD contract, then codes their implementation against it
4. **Integrate against the contract**. When both sides are ready, integration testing verifies they match the contract

This pattern works because TDD interfaces are required to be "concrete enough to implement without interpretation". Which also means they are concrete enough to mock without interpretation.

### What makes a contract stub-ready

A TDD interface contract enables parallel development when it includes:
- **Complete input schemas**: the stub can validate incoming data
- **Complete output schemas**: the stub can return realistic responses
- **All error modes**: the stub can simulate failure scenarios
- **Boundary identification**: developers know which SAD component owns each side

If a developer cannot write a working stub from the TDD contract alone, the contract is not specific enough.

### Using WDD for coordination

WDD work items that cross component boundaries include an **Interface Contract Reference** identifying the specific TDD §4 contract that governs the boundary. This makes dependencies explicit:

- The developer implementing the *provider* side knows exactly what contract to satisfy
- The developer implementing the *consumer* side knows exactly what to mock
- The WDD dependency chain shows which items share a contract boundary

When planning sprints, use the Interface Contract Reference to identify work items that can proceed in parallel (different sides of the same contract) versus items that must be sequential (same side, different layers).

### When contracts change

If a TDD contract needs to change after freeze, the standard re-entry protocol applies:
1. Impact analysis identifies all work items referencing that contract
2. Both sides of the contract are re-validated
3. Any stubs or mocks built against the old contract must be updated

This is why freezing the TDD before execution matters. It prevents the contract from shifting under developers who are already coding against it.

## Common failure modes

Watch for:
- “Just this once” scope expansion
- Validators being bypassed silently
- WDD items growing beyond atomic size
- Non-goals being treated as suggestions
- Teams copying examples without adapting context

These are signals to tighten enforcement, not loosen it.

## Final guidance

aieos-engineering-execution is intentionally opinionated where it matters.

Adapt the **edges**, not the **core**.

If you preserve:
- Clear intent
- Explicit scope
- Hard gates
- Atomic execution

Then AI-assisted delivery becomes predictable, safe, and scalable.
