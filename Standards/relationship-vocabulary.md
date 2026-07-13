---
name: relationship-vocabulary
description: A small controlled vocabulary for how identified artifacts (Standards/identifier-scheme.md) reference each other, structured now so a future triple-store/SPARQL migration is additive rather than a rewrite.
status: established 2026-07-12 as a recording convention only — no triple store, no tooling, no export pipeline exists or is planned near-term
last-updated: 2026-07-12
---

# Relationship Vocabulary

## Why this exists — and why it isn't a task

Bill's stated vision (2026-07-12, explicitly flagged as deep backlog, not
current work): eventually, every architecture deliverable across every
project could live in a triple store, queryable with SPARQL, navigable
"up, down, and sideways" through the whole architecture. Nothing here
builds that. The only thing worth doing *now* is making sure today's
standards don't have to be redesigned later to support it — i.e.,
avoiding a migration that has to rewrite history instead of just adding
an export step on top of it.

The one property a triple store actually needs that prose text doesn't
give it: relationships between artifacts as **named, structured edges**
(a predicate connecting two IDs), not sentences a human has to
re-interpret. That's the entire scope of this document.

## The vocabulary

A starter set, not a closed list — extend it here when a real
relationship doesn't fit, the same way `Standards/identifier-scheme.md`'s
TYPE table grows.

| Predicate | Direction | Meaning |
|-----------|-----------|---------|
| `partOf` | up | This artifact is contained within a larger one (e.g. a Requirement Definition is `partOf` a Use Case). |
| `realizes` | down, diagram -> document type | A diagram artifact depicts/implements a document-type artifact (e.g. a Sequence Diagram `realizes` a Use Case). |
| `satisfies` | up, implementation -> requirement | An artifact fulfills the need described by a requirement (classic requirements-traceability link). |
| `collaboratesWith` | sideways | Peer relationship between two artifacts at the same level — this is the same concept already used today as the "Collaborators:" field throughout `rosetta-stone-AI`; not a new idea, just the same relationship made identifier-addressable instead of name-only. |
| `dependsOn` | sideways/down | One artifact requires another to exist or hold true. |
| `tracesTo` | up | General traceability pointer, for links that don't fit a more specific predicate above. |
| `supersedes` / `supersededBy` | lifecycle | An artifact replaces an earlier one. Use this instead of deleting or renumbering a retired ID — sequence numbers are never reused (`Standards/identifier-scheme.md`). |

"Up, down, sideways" (Bill's framing) map onto these directly: `partOf`/
`satisfies`/`tracesTo` go up toward broader context, `realizes` goes down
toward implementation, `collaboratesWith`/`dependsOn` go sideways between
peers.

## How to record a relationship today

When an artifact with a real minted ID needs to reference another one,
record it as structured frontmatter, not only in prose:

```yaml
id: RD_RSAI_0001
relationships:
  partOf: [UC_RSAI_0001]
  satisfiedBy: [SCM_RSAI_0003]
```

Each `(subject id, predicate, object id)` triple this produces is already
exactly what a triple store would want — the only thing a future
migration adds is a script that walks this frontmatter and emits it as
RDF, not a redesign of how relationships are written down. Prose
explaining *why* the relationship holds is still encouraged alongside
the frontmatter — the structured field is for machines, the prose is
still for the next human reader.

Not built yet: this convention has no real artifacts to apply to so far
(everything in `Architecture/rosetta-stone-AI-Architecture/` is still a
placeholder). Apply it starting with the first artifact that gets a real
minted ID, rather than retrofitting placeholders that don't need it yet.
