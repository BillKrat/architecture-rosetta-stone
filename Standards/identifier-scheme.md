---
name: identifier-scheme
description: The TYPE_SCOPE_SEQ unique-identifier format used across every map, document, and artifact in this development domain — not scoped to any one project.
status: established 2026-07-12; type/scope registries open for extension
last-updated: 2026-07-12
---

# Identifier Scheme

Every requirement, use case, diagram, and architecture deliverable across
every project Bill and Claude build together gets one unique, permanent
identifier. The goal (Bill's framing, 2026-07-12): an unambiguous
reference that means the same thing in any map, document, or artifact it
appears in — no context needed to know exactly what's being pointed at.
This matters more than usual because the end product is a "starter kit"
other developers' organizations need to be able to trust — an
inconsistent or ambiguous identifier scheme would undermine that trust
directly, not just be an internal inconvenience.

## Format

```
<TYPE>_<SCOPE>_<SEQ>
```

- **TYPE** — a short code for what kind of thing this is (see registry
  below). All caps.
- **SCOPE** — a short code for which project/concern it belongs to (see
  registry below). All caps.
- **SEQ** — a zero-padded sequence number, **4 digits**, e.g. `0001`.
  Unique within its `(TYPE, SCOPE)` pair; never reused, even if the thing
  it identifies is later retired — mark retired IDs as superseded (see
  `Standards/relationship-vocabulary.md`, `supersedes`/`supersededBy`),
  don't recycle the number.

Example: `RD_RSAI_0001` = the 1st Requirement Definition in the RSAI
(Rosetta Stone AI) scope.

**Resolved 2026-07-12 (Claude's recommendation, per Bill's delegation):**
Bill's original seed example mixed 5 digits (`UC_RSAI_00001`) and 4
digits (`RD_RSAI_0001`) — read as a typo, not an intentional
per-type width. Standardized on **4 digits for every type**, no
exceptions. 9,999 identifiers per `(TYPE, SCOPE)` pair is more than
enough headroom; if a pair ever approaches that limit it's worth
questioning why one bucket got so large, not just widening the number.

## TYPE registry

Two families: document/definition types (things you'd write), and
diagram types (things you'd draw — often used to *realize* a
document-type artifact; see the relationship vocabulary for how those
link together). Neither list is closed — add a row here, in this same
table, whenever a genuinely new type is needed. Don't invent a
one-off code inline in some other document.

**Resolved 2026-07-12:** Bill's seed example used `RD` for a single
requirement statement ("the widget should turn when touched"), but the
obvious expansion of "RD" is "Requirements *Document*" — the thing that
*collects* many requirements (what's called "Business Requirements
Document" in `Architecture/rosetta-stone-AI-Architecture/requirements-and-use-cases.md`).
Those are two different things that need two different codes. Resolved
as: **RD = Requirement Definition** (one atomic requirement, matches
Bill's example exactly), **BRD = Business Requirements Document** (the
containing deliverable).

### Document / definition types

| Code | Meaning | Maps to (Architecture category) |
|------|---------|----------------------------------|
| BRD  | Business Requirements Document | Requirements & Use Cases |
| FS   | Functional Specification | Requirements & Use Cases |
| US   | User Story | Requirements & Use Cases |
| UC   | Use Case | Requirements & Use Cases |
| RD   | Requirement Definition (one atomic requirement) | Requirements & Use Cases |
| DM   | Data Model | Logical Architecture |
| PD   | Process Diagram | Logical Architecture |
| SCM  | System Component Model | Logical Architecture |
| TC   | Technology Choice | Physical & Technical Specs |
| API  | API Contract | Physical & Technical Specs |
| ITM  | Infrastructure Topology Mapping | Physical & Technical Specs |
| SEC  | Security Model | System Policies |
| IDM  | Identity Model | System Policies |
| ACM  | Access Control Model | System Policies |
| DRP  | Disaster Recovery Plan | Operational Plans |
| MS   | Monitoring Strategy | Operational Plans |
| RRP  | Rollout / Rollback Plan | Operational Plans |
| RSK  | Risk / Known Issue | Risks & Open Issues *(added 2026-07-12 — cross-cutting, not one of the original 5 MSDN categories; a risk can concern any node or any other category, so it gets its own file rather than being forced into one)* |

### Diagram / notation types

Cross-cutting — not owned by one Architecture category, since a given
diagram type can support any of them (e.g. a Sequence Diagram can realize
a Use Case, or illustrate a Process).

| Code | Meaning |
|------|---------|
| SD   | Sequence Diagram |
| CD   | Class Diagram |
| AD   | Activity Diagram |
| SMD  | State Machine Diagram |
| ERD  | Entity-Relationship Diagram |
| CompD | Component Diagram |
| DFD  | Data Flow Diagram |

Both tables are a first pass, presented for correction — add, rename, or
remove rows as real work surfaces a need, rather than pre-inventing types
nothing uses yet.

## SCOPE registry

One entry per project/concern. Register a scope code here *before* its
first ID gets minted — don't invent one inline.

| Code | Project / concern |
|------|---------------------|
| RSAI | rosetta-stone-AI — the AI-system Responsibility vocabulary and its `-Architecture` companion |

Future scopes (e.g. for `vs-mcp-bridge` itself once gap-analysis/design
work starts against `rosetta-stone-MCP-Bridge`, or for any other
application) get added here when that work actually begins — not
reserved speculatively ahead of need.

## Uniqueness and collision avoidance

No central ID-issuing server exists, and Bill runs multiple parallel
Claude Code sessions against this repo. The practical safeguard: **always
read the current registry (see below) immediately before minting a new
ID**, and let git itself be the collision detector — if two sessions
mint the same next number for the same `(TYPE, SCOPE)` pair at the same
time, committing the registry produces a merge conflict, which surfaces
the collision immediately rather than silently. No additional tooling
needed for this to work; it's the same property that already makes git
a safety net for this whole project.

## Where minted IDs live

**First real IDs minted 2026-07-12:** `RD_RSAI_0001`, `RD_RSAI_0002`
(`Architecture/rosetta-stone-AI-Architecture/requirements-and-use-cases.md`)
and `RSK_RSAI_0001` through `RSK_RSAI_0005`
(`Architecture/rosetta-stone-AI-Architecture/risks-and-open-issues.md`) —
formalizing the single-owner-per-Responsibility principle and the 5
findings from the ownership audit against the frozen `rosetta-stone-AI`
map. `Standards/ID-Registry/RSAI.md` (a lean pointer list: ID, one-line
title, link, status — mirroring `INDEX.md`'s own map-not-content rule)
should be created the next time a batch of new RSAI IDs is minted, once
there's enough volume that scanning the category files directly stops
being fast enough. Not urgent at 7 IDs.
