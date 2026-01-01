# ai-sdlc-kit

**AI-assisted templates, validators, and workflows for moving through SDLC.**

---

## What This Is

**ai-sdlc-kit** is a practical, open toolkit for teams that want to use AI safely and effectively across the **software development lifecycle (SDLC)**.

It provides:
- Lean, AI-first artifact templates
- Strict, non-prescriptive validators
- A repeatable promotion and freeze model
- Examples that show how everything fits together

This repository focuses on **process and artifacts**, not tools or implementations.

---

## What Problem This Solves

AI is very good at generating content —
but without structure and gates, it creates:
- Ambiguity
- Scope creep
- Overdesign
- Unexecutable work
- Fragile delivery

**ai-sdlc-kit** addresses this by enforcing:
- Clear intent before generation
- Explicit scope and non-goals
- Deterministic handoffs between stages
- Hard validation gates before execution

The result is **predictable delivery**, even with AI in the loop.

---

## Who This Is For

- Software engineers
- Platform and DevOps engineers
- Architects
- Technical leads
- Teams experimenting with AI-assisted delivery
- Organizations that need governance without bureaucracy

You do **not** need a specific toolchain to use this kit.

---

## What’s Included

### 📄 Artifact Templates
- PRD (Product Requirements Document)
- ACF (Architecture Context File)
- SAD (System Architecture Design)
- DCF (Design Context File)
- TDD (Technical Design Document)
- WDD (Work Design Document)
- Jira story templates

Each template is designed to be:
- Passed directly to an AI
- Easy to validate
- Hard to misuse

---

### ✅ Validators
Strict, non-prescriptive validators that act as **quality gates**:
- PRD Validator
- SAD Validator
- TDD Validator
- WDD Validator
- Definition of Ready (DoR) Validator

Validators **do not redesign or suggest solutions** —
they only determine readiness.

---

### 📘 Playbook
A canonical, end-to-end playbook that defines:
- Artifact flow and promotion rules
- Refinement ladders
- Freeze points
- Intent alignment checkpoints
- Enforcement responsibilities

---

### 🧪 Examples
Anonymized, end-to-end examples showing:
- How artifacts evolve from PRD to execution
- How validators pass or fail
- What “good” looks like in practice

---

## Core Principles

- **AI generates, validators decide**
- **Artifacts are promoted, not rewritten**
- **Execution artifacts are stricter than design artifacts**
- **Ambiguity is a failure condition**
- **Non-goals are enforceable**

These principles are applied consistently across the repository.

---

## Quickstart

1. Start with a PRD defining intent, scope, and non-goals
2. Run an **Intent Summary pre-pass** to confirm understanding
3. Generate the next artifact using the provided template
4. Run the corresponding validator
5. Fix blocking issues only
6. Freeze and promote the artifact
7. Repeat until you reach execution-ready Jira stories

See **`docs/index.md`** to get started.

---

## Documentation

All documentation lives in the `docs/` directory:

- **Start here:** `docs/index.md`
- **Playbook:** `docs/playbook.md`
- **Templates:** `docs/artifacts/`
- **Validators:** `docs/validators/`
- **Examples:** `examples/`

---

## Anonymization & Safety

This is a **public repository**.

All content:
- Is employer-neutral
- Uses placeholders instead of real identifiers
- Avoids internal systems, URLs, and names

See **`ANONYMIZATION.md`** before contributing.

---

## Contributing

Contributions are welcome.

Please read:
- `CONTRIBUTING.md`
- `TERMS.md`
- `ANONYMIZATION.md`

Small, focused improvements are preferred.

---

## License

This project is licensed under the MIT License.

---

## Final Note

This kit is intentionally disciplined.

If something feels “heavy,” it’s usually because it prevents downstream chaos.

If something feels “light,” it’s because it’s meant to be reused safely.

