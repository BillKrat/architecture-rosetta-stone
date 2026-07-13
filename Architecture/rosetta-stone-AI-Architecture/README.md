# rosetta-stone-AI-Architecture

Companion BDUF document to `rosetta-stone-AI` (the Responsibility vocabulary —
see `Artifacts/XMind/rosetta-stone-AI.xmind`). Where `rosetta-stone-AI`
establishes *what each node's job is and who it collaborates with*, this
document is the living, MSDN-style container for *the concrete deliverables*
that turn that vocabulary into a buildable system — requirements, logical
design, technical specs, policies, and operational plans. Both evolve
together; this one is never frozen.

Part of the path toward `vs-mcp-bridge`, an open-source MCP developer
starter kit — this document exists to leave a future developer enough
context to pick up the work cold, not just to satisfy process.

**This file is a map, not content** — same rule as the repo root
`INDEX.md`. One line per category and a link; the actual artifact list,
summaries, and status live in each category's own file.

## Categories

- [Requirements & Use Cases](requirements-and-use-cases.md) — Business Requirements Document, Functional Specifications, User Stories
- [Logical Architecture](logical-architecture.md) — Data Models, Process Diagrams, System Component Models
- [Physical & Technical Specs](physical-and-technical-specs.md) — Technology Choices, API Contracts, Infrastructure Topology Mappings
- [System Policies](system-policies.md) — Security Model, Identity Model, Access Control Model
- [Operational Plans](operational-plans.md) — Disaster Recovery (DR) Plans, Monitoring Strategy, Rollout / Rollback Plan

## Status

Scaffolded 2026-07-12. Every artifact type below currently holds a
first-pass summary of *what it's meant to collect*, not real content —
`rosetta-stone-AI` itself is still mid Phase 1 training (see
`../../Topics/bduf-freeze-and-training.md`), so this document's actual
content should mature alongside that vocabulary as it gets signed off,
not race ahead of it.

## Naming convention

`rosetta-stone-<Concern>-Architecture`, sibling folders under
`Architecture/` — one per concern document in the main map set. The next
one anticipated is `rosetta-stone-MCP-Bridge-Architecture`, once
gap-analysis/design work starts for `vs-mcp-bridge` against the frozen
`rosetta-stone-MCP-Bridge` document.

## Identifiers

Every artifact in the category files below gets a unique ID once it has
*real* content (scope code `RSAI`) — see `../../Standards/identifier-scheme.md`
for the format and type codes, and `../../Standards/relationship-vocabulary.md`
for how to record a relationship to another artifact. Placeholders don't
get IDs minted yet; that happens as each one is actually authored.
