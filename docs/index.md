# ai-sdlc-kit Documentation

Welcome to **ai-sdlc-kit** — a practical toolkit for using AI safely across the full **software development lifecycle (SDLC)**.

This documentation explains **how to use the kit**, **why it works**, and **how the pieces fit together**.

---

## Start Here

If you’re new to the kit, follow this order:

1. **Understand the process**
   - Read the **Playbook** to learn the end-to-end flow, gates, and freeze points.

2. **Use the templates**
   - Generate SDLC artifacts using the **AI-first templates**.

3. **Apply validators**
   - Run validators to determine readiness before promotion.

4. **Learn by example**
   - Walk through the anonymized, end-to-end examples.

---

## Core Concepts

The kit is built on a few simple ideas:

- **AI generates, validators decide**
- **Artifacts are promoted, not rewritten**
- **Execution artifacts are stricter than design artifacts**
- **Ambiguity is a failure condition**
- **Non-goals are enforceable**

These principles are applied consistently across all artifacts and validators.

---

## Documentation Sections

### 📘 Playbook
Defines the canonical process:
- Artifact flow and promotion rules
- Refinement ladders
- Freeze points
- Intent Summary pre-pass
- Enforcement responsibilities

➡️ See: `playbook.md`

---

### 📄 Artifact Templates
Lean, AI-first templates for each SDLC stage:
- PRD
- ACF
- SAD
- DCF
- TDD
- WDD
- Jira story templates

Templates are designed to:
- Be passed directly to AI
- Produce consistent structure
- Be easy to validate

➡️ See: `artifacts/`

---

### ✅ Validators
Strict, non-prescriptive readiness gates:
- PRD Validator
- SAD Validator
- TDD Validator
- WDD Validator
- Definition of Ready (DoR) Validator

Validators determine **readiness**, not correctness or implementation quality.

➡️ See: `validators/`

---

### 🧪 Examples
Anonymized examples showing:
- Artifact evolution from PRD to execution
- Validator PASS/FAIL outputs
- What “good” looks like in practice

➡️ See: `../examples/`

---

## How to Use This Kit with AI

A typical flow looks like this:

1. Provide the AI with:
   - The upstream artifact
   - The relevant template
   - Any applicable context files (ACF, DCF)

2. Run the **Intent Summary pre-pass** to confirm understanding.

3. Generate the artifact using the template.

4. Run the corresponding validator.

5. Fix only blocking issues.

6. Freeze and promote the artifact.

Repeat until you reach execution-ready work.

---

## Anonymization & Safety

This is a public repository.

All examples and templates:
- Avoid real company names
- Use placeholders for identifiers
- Remain tool- and employer-neutral

Before contributing, read:
- `ANONYMIZATION.md`
- `TERMS.md`

---

## Contributing

Contributions are welcome.

Please see:
- `CONTRIBUTING.md`
- `CODE_OF_CONDUCT.md`
- `SECURITY.md`

Small, focused improvements are preferred.

---

## Where to Go Next

- Read the **Playbook** → `playbook.md`
- Browse **Templates** → `artifacts/`
- Review **Validators** → `validators/`
- Explore **Examples** → `../examples/`

---

This kit is intentionally disciplined.

The structure you see here exists to make AI-assisted delivery **predictable, safe, and repeatable**.
