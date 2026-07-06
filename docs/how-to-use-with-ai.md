# How to Use aieos-engineering-execution with AI

This guide explains how to use the kit's prompts, templates, and validators with an AI assistant to generate and validate SDLC artifacts.

---

## Setting Up Your AI Tool

Most AI coding tools support project-level instruction files that are loaded automatically at the start of every session. Use these to give the AI persistent awareness of the kit and your project's conventions.

| Tool | Instruction File | Location |
|------|-----------------|----------|
| Claude Code / VS Code (Claude) | `CLAUDE.md` | Project root |
| Cursor | `.cursorrules` | Project root |
| Windsurf | `.windsurfrules` | Project root |
| Other tools | Check tool documentation | Varies |

### What to Include in Your Project Instruction File

At minimum, your instruction file should tell the AI:

1. **Where the kit lives**. Path or reference to the kit's prompts, specs, templates, and validators
2. **Where artifacts live**. Your project's `docs/sdlc/` directory structure
3. **The artifact flow**. The non-negotiable promotion order (PRD → ACF → SAD → DCF → TDD → WDD → Execute → ORD)
4. **Key constraints**. Freeze-before-promote, one artifact per session, validators as hard gates

If the kit is a separate repository, reference it by path. If copied into your project, reference the local directory.

### Example Instruction File Entry

```
## SDLC Kit

This project uses aieos-engineering-execution for structured artifact generation and validation.

Kit location: ../aieos-engineering-execution/docs/
Project artifacts: docs/sdlc/

Artifact flow: PRD → ACF → SAD → DCF → TDD → WDD → Execute → ORD
- Each artifact must be frozen before downstream artifacts are generated
- Use a separate AI session for generation and validation
- Validators are hard gates, any failure means FAIL

See the kit's playbook.md for the full process definition.
```

This ensures every AI session. regardless of tool. starts with the right context without requiring you to re-explain the kit each time.

## The Core Pattern

Every artifact follows the same three-step pattern:

1. **Generate**. Give the AI a prompt and inputs; it produces the artifact
2. **Validate**. Give the AI the validator and the artifact; it returns PASS or FAIL
3. **Freeze**. Once PASS and human-approved, the artifact is locked

Each step is a separate AI session. This keeps context clean and prevents the AI from conflating artifacts.

## Generating an Artifact

Start a new AI session and provide:

1. **The spec**. The `{type}-spec.md` file that defines content rules, format requirements, and hard gates
2. **The generation prompt**. The `{type}-prompt.md` file for the artifact you're generating
3. **The template**. The `{type}-template.md` file so the AI follows the exact structure
4. **The frozen upstream artifacts**. The inputs listed in the prompt

### Example: Generating a SAD

> Here is the specification for a System Architecture Design:
>
> [paste contents of `sad-spec.md`]
>
> Here is the prompt for generating a System Architecture Design:
>
> [paste contents of `sad-prompt.md`]
>
> Here is the template to follow:
>
> [paste contents of `sad-template.md`]
>
> Here are the frozen upstream artifacts:
>
> **PRD:**
> [paste frozen PRD]
>
> **ACF:**
> [paste frozen ACF]
>
> Generate the SAD following the template exactly.

The AI will produce a SAD that follows the template structure, satisfies the spec's content rules, traces to the PRD, and respects ACF guardrails.

### Tips for Generation

- **One artifact per session.** Don't generate a PRD and SAD in the same session. Context bleeds and quality drops.
- **Paste the full upstream artifacts.** Don't summarize: the AI needs the details to trace requirements correctly.
- **Include the spec.** The spec defines what quality criteria the content must satisfy. Without it, the AI relies only on embedded prompt rules.
- **Include the template.** Without it, the AI may invent its own structure, making validation harder.
- **Don't prompt the AI to be creative.** The prompts are designed to constrain output. Let them work.

## Validating an Artifact

Start a **new** AI session (not the one that generated the artifact) and provide:

1. **The spec**. The `{type}-spec.md` file that defines the evaluation criteria
2. **The validator**. The `{type}-validator.md` file
3. **The artifact to validate**. The generated artifact

### Example: Validating a SAD

> Here is the specification for a System Architecture Design:
>
> [paste contents of `sad-spec.md`]
>
> Here is the validator for a System Architecture Design:
>
> [paste contents of `sad-validator.md`]
>
> Here is the SAD to validate:
>
> [paste the generated SAD]

The AI will return structured JSON:

```json
{
  "status": "PASS | FAIL",
  "hard_gates": { ... },
  "blocking_issues": [ ... ],
  "warnings": [ ... ],
  "completeness_score": 85
}
```

### Why a Separate Session?

If the same AI that generated the artifact also validates it, it has a bias toward passing its own work. A fresh session with only the validator rules and the artifact produces a more honest evaluation.

### Starting a Validation Session. Step by Step

"New session" means:

1. **End the generation session.** Close the conversation or start a new one. Do not continue in the same thread.
2. **Open a fresh conversation.** No prior context should carry over. Project-level instructions (CLAUDE.md) are fine. They don't contain artifact content.
3. **Do not include generation inputs.** The generation session contained the spec + prompt + template + principles. Leave all of these out. The validator is the only behavior instruction needed.
4. **Paste in this order:**
   - The spec (`{type}-spec.md`)
   - The validator (`{type}-validator.md`)
   - Frozen upstream artifacts if the validator requires them for traceability (e.g., TDD + ACF + DCF for ORD validation)
   - The artifact to validate
5. **Give a single instruction:** "Validate this artifact against the spec and validator. Output JSON only."
6. **Review the output**. If status is fail, address only the blocking issues listed. do not redesign.
7. **Re-run in a new session** after fixes (same rules apply).

### Handling FAIL Results

1. Review the `blocking_issues`. each one identifies a specific gate, description, and location
2. Fix only the blocking issues in the artifact (do not redesign)
3. Re-run the validator in a new session
4. If the same gate keeps failing after two cycles, the root cause may be in an upstream artifact. See the re-entry protocol in the playbook

## Inputs by Artifact Type

| Artifact | Spec | Prompt | Inputs |
|----------|------|--------|--------|
| PRD | `prd-spec.md` | `prd-prompt.md` | Product brief (human-written) |
| ACF | `acf-spec.md` | `acf-prompt.md` | Architecture Context intake form (`architecture-context-template.md`) + engineering principles (`code-craftsmanship.md` §2) |
| SAD | `sad-spec.md` | `sad-prompt.md` | Frozen PRD + Frozen ACF. Brownfield: + System Context intake form (`system-context-template.md`) |
| DCF | `dcf-spec.md` | `dcf-prompt.md` | Design Context intake form (`design-context-template.md`) + engineering principles (`code-craftsmanship.md`) + product principles (`product-craftsmanship.md`) |
| TDD | `tdd-spec.md` | `tdd-prompt.md` | Frozen SAD + Frozen DCF |
| WDD | `wdd-spec.md` | `wdd-prompt.md` | Frozen TDD |
| ORD | `ord-spec.md` | `ord-prompt.md` | Frozen TDD + Frozen ACF + Frozen DCF |

For validation, the input is always: the spec + the validator + the artifact being validated.

The DoR Validator (`dor-validator.md`) is run per WDD work item, not against the full WDD.

### Utility Prompts

These prompts produce input material or advisory outputs. They are not governed artifacts with specs or validators.

| Prompt | Purpose | Inputs |
|--------|---------|--------|
| `greenfield-intake-prompt.md` | Facilitate ACF and DCF intake form completion for greenfield projects | Frozen PRD + optional team notes |
| `codebase-analysis-prompt.md` | Pre-fill intake forms for brownfield projects | Existing codebase |
| `impact-analysis-prompt.md` | Assess downstream effects before modifying a frozen artifact | Frozen artifacts + proposed change |
| `mock-impact-prompt.md` | Identify existing test files that need mock updates when a work item changes a shared interface | WDD work item + TDD §4 + existing test files |
| `work-group-gate-prompt.md` | Verify work group gate conditions and produce the gate artifact file | WDD work group + Phase 4 review files + test results |
| `bat-prompt.md` | Generate business acceptance testing protocol and results template for a work group | WDD work group + member items |
| `team-composition-prompt.md` | Derive team roles, skills, and deliverables from work items | Frozen WDD + Frozen TDD (recommended) |
| `wdd-csv-export-prompt.md` | Export WDD work items as CSV for import into work management tools | Frozen WDD + optional field mapping override |

## The Execution Loop

Once WDD work items pass the DoR Validator, they enter the execution loop. Each phase uses its own prompt:

| Phase | Prompt | What You Provide |
|-------|--------|-----------------|
| Tests | `test-prompt.md` | WDD work item + TDD testing strategy + DCF testing expectations |
| Plan | `plan-prompt.md` | Approved test specs + TDD interface contracts + relevant source code |
| Code | `code-prompt.md` | Approved plan + approved test specs + WDD work item + ACF guardrails + source code |
| Review | `review-prompt.md` | Completed code + test results + WDD acceptance criteria + ACF guardrails |

Each phase is a separate AI session. The human approves the output of each phase before the next one begins.

**Important:** The execution phase prompts reference `execution-spec.md` for iteration rules, escalation criteria, and completion verification. Include the execution spec as context when running code and review phases so the AI follows the correct protocols for failure handling and scope control.

### Generating the Execution Plan

Before starting the execution loop, generate the execution plan, then use the phase-specific prompts to assemble ready-to-use prompts for each phase. One phase at a time.

**Step 1: Generate the execution plan**

> [paste contents of `execution-plan-prompt.md`]
>
> **Frozen WDD:** [paste frozen WDD]
>
> **Frozen TDD:** [paste frozen TDD]
>
> **Frozen ACF:** [paste frozen ACF]
>
> **Frozen DCF:** [paste frozen DCF]

This produces an execution order and per-work-item context (relevant TDD/ACF/DCF sections extracted per item). Save the output.

**Step 2: Assemble Phase 1 (Tests) prompts**

> [paste contents of `execution-plan-tests-prompt.md`]
>
> **Approved Execution Plan:** [paste execution plan output]

This produces assembled, ready-to-use test prompts for each work item. Run each one in a separate AI session. Approve the test specifications.

**Step 3: Assemble Phase 2 (Plan) prompts**

> [paste contents of `execution-plan-plan-prompt.md`]
>
> **Approved Execution Plan:** [paste execution plan output]
>
> **Approved Phase 1 Output:** [paste approved test specs per work item]

This produces assembled plan prompts with test specs included. Run, approve.

**Step 4–5: Repeat for Code and Review**

Use `execution-plan-code-prompt.md` (after Phase 2) and `execution-plan-review-prompt.md` (after Phase 3) the same way, each takes the execution plan plus the approved outputs from previous phases and produces ready-to-use prompts.

Each phase prompt assembles everything. No manual input gathering needed.

## Practical Workflow Summary

```
Session 1:  spec + prompt + template + inputs  →  generated artifact
Session 2:  spec + validator + artifact        →  PASS/FAIL JSON
            (if FAIL: fix, then new Session 2)
Session 3:  human reviews, approves, freezes
            → move to next artifact
```

Repeat for each artifact in the flow: PRD → ACF → SAD → DCF → TDD → WDD → Execute → ORD.

## Common Mistakes

**Dumping everything into one session.** The AI loses focus. Keep sessions artifact-scoped.

**Skipping the spec.** Without the spec, the AI doesn't know what content rules and quality criteria to satisfy. The validator may still catch issues, but generation quality suffers.

**Skipping the template.** Without a template, the AI structures the artifact however it wants, and the validator flags structural issues.

**Validating in the same session that generated.** The AI is biased toward its own output. Use a fresh session.

**Fixing warnings during validation.** Warnings are non-blocking. Fix only blocking issues unless a warning reveals a real problem.

**Summarizing upstream artifacts.** Paste the full frozen artifact. Summaries lose the detail that validators check for traceability.

**Letting the AI run the full flow autonomously.** The human is the orchestrator. The AI generates and validates one artifact at a time. Human judgment is the final gate at every step.
