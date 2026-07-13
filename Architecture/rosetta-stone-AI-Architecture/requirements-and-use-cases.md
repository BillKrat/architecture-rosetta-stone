---
name: requirements-and-use-cases
description: Business requirements, functional specifications, user stories, use cases, and individual requirement definitions for the rosetta-stone-AI system.
status: mixed — Requirement Definitions has real content (2 entries); everything else still placeholder
last-updated: 2026-07-12
---

# Requirements & Use Cases

The "why we're building this, what it must do, and how someone actually
experiences it" layer — grounded in `rosetta-stone-AI`'s Responsibility
vocabulary once that's signed off, not a re-derivation of it.

## Business Requirements Document

**What this collects:** The problem this AI system exists to solve, who
it serves, and the business-level success criteria — independent of any
implementation choice. The "why build this at all" answer that everything
else in this Architecture document should trace back to.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## Functional Specifications

**What this collects:** What the system must actually do, expressed in
terms of the Responsibilities and behaviors `rosetta-stone-AI` already
establishes per node (Application, Model, Agent, Tool, Retrieval, Memory,
Security, etc.) — a specification of behavior, not a redefinition of the
vocabulary itself.

**Status:** Not started — blocked on `rosetta-stone-AI` Phase 1 sign-off
(see `Topics/bduf-freeze-and-training.md`).

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## User Stories

**What this collects:** Concrete "as a [role], I want [capability], so
that [outcome]" scenarios grounded in the Application node's actual
user-facing behavior — used to sanity-check that the Responsibility
vocabulary produces sensible real-world behavior, not just internally
consistent definitions.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## Use Cases

**What this collects:** Concrete, bounded scenarios of a user or system
accomplishing a goal via `rosetta-stone-AI` — the `UC` type in
`../../Standards/identifier-scheme.md`. None minted yet, deliberately:
a real Use Case should come out of Phase 1 training producing an actual
scenario, not be invented here just to fill the category.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## Requirement Definitions

Individual, atomic requirement statements (`RD` type) — as distinct from
the Business Requirements Document above, which is the deliverable that
*collects* many of these, not one itself. The two entries below are the
first real (non-placeholder) content in this whole Architecture
document: governance requirements against `rosetta-stone-AI`'s own
vocabulary, formalized 2026-07-12 out of this session's ownership audit.
See `risks-and-open-issues.md` for the specific findings that currently
violate them.

### RD_RSAI_0001 — Every Responsibility has exactly one Owner

```yaml
id: RD_RSAI_0001
type: RD
scope: RSAI
status: active
basis: claude-reasoning
rationale: >
  Originated as Bill's stated assumption ("in a well designed framework,
  there will be only one owner of a responsibility") — per
  Standards/source-of-truth.md, that alone isn't sufficient basis. What
  actually grounds this as a requirement: it's the same rule the RACI
  framework enforces for its "Accountable" role (exactly one party, never
  zero, never more than one) applied here by analogy to Responsibility
  ownership, not verified against a specific citable standard. Upgrade
  to `authoritative` if a specific citable source is sourced later.
relationships:
  satisfiedBy: []
```

Every node in `rosetta-stone-AI` (and, by extension, any future
`rosetta-stone-<Concern>` vocabulary) must have exactly one named,
accountable Owner — never zero, never more than one. This is Bill's own
stated assumption from this session, formalized rather than paraphrased:
"in a well designed framework, there will be only one owner of a
responsibility."

**Status:** Active — not yet fully satisfied. See `RSK_RSAI_0001` in
`risks-and-open-issues.md`.

**Owner:** (unassigned — this requirement is about `rosetta-stone-AI`'s
governance, not itself part of that vocabulary; needs a BDUF-process
owner, not an AI-system-node owner)

### RD_RSAI_0002 — Every concern is defined in exactly one place

```yaml
id: RD_RSAI_0002
type: RD
scope: RSAI
status: active
basis: claude-reasoning
rationale: >
  Claude's own synthesis from the pattern across this session's 4
  duplication-type findings (RSK_RSAI_0002-0005) — not Bill's direct
  words, and not verified against a specific citable standard. Informally
  echoes well-known non-duplication/single-source-of-truth principles
  (e.g. DRY, and requirements-engineering guidance on avoiding
  conflicting/duplicate requirements) but that's context, not a citation.
  Flag if this shouldn't stand as its own rule separate from
  RD_RSAI_0001.
relationships:
  satisfiedBy: []
```

Any given concern or capability (e.g. a deployment context, a
provenance/grounding rule, a data-handling policy) must be defined and
owned in exactly one place in the vocabulary — not duplicated or
independently claimed by more than one node. Distinct from
`RD_RSAI_0001`: that one is about a node having *at least and at most
one* owner; this one is about a *concern* not being modeled twice under
two different nodes (each of which might individually satisfy
`RD_RSAI_0001` on its own, while still violating this one together).
This requirement is Claude's synthesis from the pattern across this
session's findings, not a direct quote from Bill — flag if it shouldn't
stand as its own rule.

**Status:** Active — not yet satisfied. See `RSK_RSAI_0002` through
`RSK_RSAI_0005` in `risks-and-open-issues.md`.

**Owner:** (unassigned — same reasoning as `RD_RSAI_0001`)
