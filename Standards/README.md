# Standards

Cross-project standards — rules meant to apply across every application
Bill and Claude build together, not scoped to `rosetta-stone-AI`
specifically. This folder is the natural home for them: the repo's own
charter already frames itself as "the method, not the boundary" (see
root `INDEX.md`), and AI is only the current test case running through
it.

**This file is a map, not content** — same rule as the root `INDEX.md`
and `Architecture/rosetta-stone-AI-Architecture/README.md`. One line per
standard and a link; the actual rules live in each standard's own file.

## Standards

- [identifier-scheme](identifier-scheme.md) — the `TYPE_SCOPE_SEQ` unique-identifier format used for every requirement, use case, diagram, and architecture deliverable across every project (established)
- [relationship-vocabulary](relationship-vocabulary.md) — controlled vocabulary + recording convention for how identified artifacts reference each other, designed so a future triple-store migration is additive (established as a convention; no tooling built or planned near-term)
- [source-of-truth](source-of-truth.md) — every artifact declares its basis (`authoritative` citation, `primary-source` quote, or explicitly-labeled `claude-reasoning`) — Bill's statements alone are never sufficient (established)
- [glossary](glossary.md) — cross-project terminology; first entry is WDNA (Windows DNA), the three-tier reference architecture now guiding component placement in `rosetta-stone-AI-Architecture` (established, one entry)

## Why this exists as its own top-level folder

Quality/consistency here isn't optional polish — Bill's framing (2026-07-12):
the end product is a "starter kit" other developers' organizations need
to trust, so human inconsistency in the standard itself is a real risk to
design against, not just an internal nuisance. Standards get the same
one-file-per-concern, index-not-content treatment as `Topics/` and
`Architecture/` for the same reason those got it: a single ever-growing
document defeats the goal of keeping any one standard easy to actually
read and apply.
