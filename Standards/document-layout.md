---
name: document-layout
description: The template every BDUF artifact document in this project follows — category files, individual artifact entries, and contributed source documents — formalizing what had been built ad hoc across Architecture/rosetta-stone-AI-Architecture/.
status: established 2026-07-13, formalizing an already-consistent pattern (not a new invention)
last-updated: 2026-07-13
---

# Document Layout

Bill's ask (2026-07-13): if an artifact type doesn't have an established
layout standard, or its existing one doesn't fit future requirements —
naming a future triple-store migration specifically, while reaffirming
that building the triple store itself stays off the backlog — establish
one, for us and for future contributors. This formalizes what was
already being done consistently across `Architecture/rosetta-stone-AI-Architecture/`
since 2026-07-12, rather than inventing something new — the three
patterns below are extracted directly from `requirements-and-use-cases.md`,
`logical-architecture.md`, `system-policies.md`, and
`risks-and-open-issues.md` as they already exist.

This file governs *shape*. `Standards/identifier-scheme.md` governs IDs,
`Standards/relationship-vocabulary.md` governs how artifacts reference
each other (and why that's triple-store-ready), `Standards/source-of-truth.md`
governs how a claim is justified. This file is where those three meet on
the page.

## Pattern 1 — Category file

One per MSDN category (or cross-cutting concern, like
`risks-and-open-issues.md`) under `Architecture/rosetta-stone-<Concern>-Architecture/`.

```markdown
---
name: kebab-case-matching-filename
description: One line — what this whole file collects.
status: Free text — e.g. "scaffolded, placeholders only" or "mixed — N real entries, rest placeholder"
last-updated: YYYY-MM-DD
---

# Category Title

1-2 paragraphs of intro: what this category is for, how it relates to
neighboring categories.

## Artifact Type Name

**What this collects:** what this artifact type is for, written for a
future developer with no other context.

**Status:** Not started. | N real entries below.

**Owner:** (unassigned) | Name/role.

**Linked artifacts:** none yet. | Pointer to the entries below.

[If real entries exist, they go here as Pattern 2 subsections]
```

Every artifact-type section gets these four fields even while empty —
don't skip a section just because it has nothing yet; an absent section
looks like an oversight, an empty one with fields filled in looks like a
deliberate placeholder.

## Pattern 2 — Individual artifact entry

A real, ID-tagged artifact, nested under its artifact-type's `##`
heading in the category file (not a separate file — several small
artifacts share one category file, per
`Standards/relationship-vocabulary.md`'s "first real use" refinement).

```markdown
### TYPE_SCOPE_SEQ — Short descriptive title

​```yaml
id: TYPE_SCOPE_SEQ
type: TYPE
scope: SCOPE
status: active | open | ...
basis: authoritative | primary-source | claude-reasoning | unverified
citation: [...]      # if basis: authoritative
quoted: "..."        # if basis: primary-source
rationale: "..."     # if basis: claude-reasoning
relationships:
  predicateName: [OTHER_ID, ...]
​```

Prose explaining the artifact — what it is, why it exists, what it
connects to. The yaml block is for machines and for a fast scan; the
prose is still for the next human reader, per
`Standards/relationship-vocabulary.md`.

**Status:** ...

**Owner:** (unassigned) | Name/role.
```

The `yaml` block is the whole point, structurally: every field in it is
already exactly what a future triple-store export needs (`id` is the
node, each `relationships` entry is a ready-made triple). Nothing about
that block should change shape when a triple store eventually exists —
only a new export step gets added on top.

## Pattern 3 — Contributed source document

A full document handed over by a person (Bill, or any future
contributor), preserved verbatim rather than dissolved into Pattern 2
entries — see `contributed-windows-dna-credential-vault-context.md` for
the first real example.

```markdown
---
name: kebab-case-matching-filename
description: What this document is and what it was extracted into.
status: contributed YYYY-MM-DD — [conceptual/final/etc, in the contributor's own framing]
last-updated: YYYY-MM-DD
---

# Contributed source document

Contributed by [name], YYYY-MM-DD, verbatim — preserved as the
primary-source this document's own words are, not paraphrased. Points
to whatever Pattern 2 entries it produced.

---

[The document, unedited, below the divider]
```

**Why keep both the verbatim document and extracted entries, rather than
just one:** the verbatim copy is the record of what was actually
contributed (if a Pattern 2 entry's summary is ever disputed, this is
what to check it against); the extracted entries are what makes the
contribution *trackable, ID-addressable, and cross-referenceable* the
same way everything else in this project is. Neither replaces the other.

## What this doesn't cover

A visual, node-based reference map (e.g. the WDNA three-tier diagram
Bill asked for next) is a different kind of artifact — a diagram for
learning and quick lookup, not a source-of-record document. It should
*point into* documents laid out per this standard, not duplicate their
content. Not built yet; next session's task.
