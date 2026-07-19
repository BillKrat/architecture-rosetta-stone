---
name: source-of-truth
description: Bill's statements are never treated as verified fact on their own — every claim needs an authoritative source, and when none exists, Claude's reasoning stands in for one only if that's explicitly labeled.
status: established 2026-07-12; extended to an unconditional cross-repo rule 2026-07-19
last-updated: 2026-07-19
---

# Source of Truth

Bill's rule, stated directly (2026-07-12): "I am 'never' the source of
truth, any thing I say needs to be verified and an authoritative source
of truth used (not someones blog). In some cases, your reasoning and
training may have to become the source of truth, if that is the case, we
have to document that somewhere; I will never be the source of truth."

This isn't about distrust — it's the same "quality first" reasoning
behind `Standards/identifier-scheme.md` and
`Standards/relationship-vocabulary.md`: the end product is a starter kit
other developers' organizations need to trust, so *where a claim came
from* has to be as traceable as the claim itself.

## The rule

Nothing in this project's architecture documents gets to rest on "Bill
said so" or "Claude thinks so" without that being visible. Every
artifact that asserts something (a Requirement Definition, a Risk, a
Data Model, anything) declares its basis explicitly.

## Basis categories

| Value | Meaning | Bar to clear |
|-------|---------|---------------|
| `authoritative` | Verified against a citable, authoritative external source — a spec, standard, official documentation, primary reference. | Must include an actual citation. "Widely known" or "I recall" doesn't qualify — and neither does a blog post, however well-written. |
| `primary-source` | Directly observed/quoted from the actual artifact being described (e.g. a finding that quotes `rosetta-stone-AI`'s own text). The system being documented is its own authority for what it currently says. | Must be a direct quote or a verifiable read of the actual source, not a paraphrase from memory. |
| `claude-reasoning` | No authoritative external source exists or was found; this is Claude's own inference, synthesis, or judgment call, informed by general training. | Must include a brief rationale explaining what it's informed by, and must be flagged as this category, not silently presented as fact. This is the case Bill's rule is most pointed at — reasoning can stand in for a source, but only in the open. |
| `unverified` | Came from Bill (or any other input) and hasn't yet been checked against the categories above. | Provisional by definition — an artifact shouldn't stay at `unverified` once it's actually relied on; upgrade it to one of the above or explicitly flag that verification was attempted and failed. |

## How to record it

Add a `basis` field to an artifact's metadata block (see
`Standards/relationship-vocabulary.md` for where that block lives):

```yaml
id: RD_RSAI_0001
basis: claude-reasoning
rationale: >
  Informed by the RACI convention that a task/deliverable has exactly one
  "Accountable" party — applied here by analogy, not verified against a
  specific citable standard.
```

For `authoritative`, `rationale` becomes `citation` and must be a real,
checkable reference. For `primary-source`, `rationale` becomes `quoted`
with the actual excerpt.

## Extended beyond this repo, unconditionally (2026-07-19)

This basis vocabulary (`authoritative`/`primary-source`/`claude-reasoning`/
`unverified`) is now also the backbone of an unconditional "Evidence
Discipline" rule in every repo's `AGENTS.md` — not just this repo's own
formal architecture artifacts. Motivated by a real incident: an AI
assistant stated an unverified hypothesis as fact during multi-subsystem
bug triage in a regulated-industry workplace, and subsequent work built
on it as settled, nearly triggering an incorrect quality/compliance
escalation.

The extension: this rule applies to *every claim about system or code
behavior in any conversation*, not only to formal artifact metadata, and
it does not require an explicit invocation to hold — unlike a triggered
skill, it is the default. `vs-mcp-bridge/.claude/skills/investigate/SKILL.md`
holds the structured, heavier procedure this rule scales up to for
formal root-cause triage or stakeholder-facing causation summaries — the
same four-category vocabulary, applied with the process a real
regulated-industry investigation needs (scope the subsystems, label
every claim as it's made, never let an unlabeled claim become
load-bearing, verify the full causal chain before concluding a root
cause).

## Why this doesn't slow things down more than it should

Most artifacts in this project so far are either direct observations of
`rosetta-stone-AI`'s own text (`primary-source`) or genuinely novel
synthesis with no existing standard to check against
(`claude-reasoning`, honestly labeled). `authoritative` will be rarer
here than in, say, a security-policy document citing an actual RFC —
that's fine. The point isn't to force everything into `authoritative`;
it's to never let something masquerade as settled when it's actually
either "the document itself says this" or "nobody's verified this yet,
including the two of us."
