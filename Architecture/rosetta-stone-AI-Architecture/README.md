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

- [Requirements & Use Cases](requirements-and-use-cases.md) — Business Requirements Document, Functional Specifications, User Stories, Use Cases, Requirement Definitions *(this last one has real content)*
- [Logical Architecture](logical-architecture.md) — Data Models, Process Diagrams, System Component Models *(this last one has real content)*
- [Physical & Technical Specs](physical-and-technical-specs.md) — Technology Choices, API Contracts, Infrastructure Topology Mappings
- [System Policies](system-policies.md) — Security Model, Identity Model, Access Control Model *(the first has real content)*
- [Operational Plans](operational-plans.md) — Disaster Recovery (DR) Plans, Monitoring Strategy, Rollout / Rollback Plan
- [Risks & Open Issues](risks-and-open-issues.md) — cross-cutting, added 2026-07-12; not one of the original 5 MSDN categories, a risk can concern any of them
- [contributed-windows-dna-credential-vault-context](contributed-windows-dna-credential-vault-context.md) — not a category, a verbatim record of a source document Bill contributed 2026-07-13; the real content it produced lives in Logical Architecture (`SCM_RSAI_0001`) and System Policies (`SEC_RSAI_0001`) above

## Status

Scaffolded 2026-07-12; first real content added the same day, more added
2026-07-13. Populated so far: `risks-and-open-issues.md` (5 findings),
`requirements-and-use-cases.md`'s "Requirement Definitions"
(`RD_RSAI_0001`, `RD_RSAI_0002`), `logical-architecture.md`'s "System
Component Models" (`SCM_RSAI_0001` — Credential Indirection and Secure
Secret Management Service, placed via WDNA's tier model, see
`../../Standards/glossary.md`), and `system-policies.md`'s "Security
Model" (`SEC_RSAI_0001` — the same service's internal responsibilities).
Everything else is still a placeholder summary of *what it's meant to
collect*, not real content. `rosetta-stone-AI` itself is still mid
Phase 1 training (see `../../Topics/bduf-freeze-and-training.md`); most
remaining content should mature alongside that vocabulary as it gets
signed off, not race ahead of it — the risks and the credential-vault
placement are both exceptions with their own independent justification
(the risks document known issues *in* the frozen vocabulary; the
credential-vault work is additive, new-component architecture that
doesn't depend on Phase 1 resolving first).

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
