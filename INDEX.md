# Rosetta Stone for Software Architecture — Index

Establish a shared, tested vocabulary for AI system architecture —
where every term names a distinct Responsibility, not an overloaded or
borrowed one — so architects can build and discuss these systems
without inheriting meaning-drift. AI is the current test case running
through the method, not the boundary of it.

**Working reference, not a gate (revised 2026-07-14):** this project's
terminology for architectural layers is **WDNA (Windows DNA)** —
Presentation / Business / Data Services. Standards documents/artifacts
follow `Standards/document-layout.md`'s templates, `Standards/identifier-scheme.md`'s
IDs, `Standards/source-of-truth.md`'s basis rule, and
`Standards/relationship-vocabulary.md`'s cross-references when producing
real Standards/Architecture content — see `Standards/README.md`. These
are working conventions to keep using, not preconditions that block
other work — see `Topics/collaborative-momentum-mode.md` for why the
"binding, not optional" framing was retired.

**This file is a map, not content.** It holds one line per topic and a
link — the actual state lives in `Topics/`. Read this in full; open a
`Topics/*.md` file only when that topic is relevant to what you're
doing.

## Active Thread

**Resume here:** `rosetta-stone-ai-node-definitions` Q&A —
[Topics/rosetta-stone-ai-node-definitions.md](Topics/rosetta-stone-ai-node-definitions.md)
(pristine reference, study from this) +
[Topics/rosetta-stone-ai-node-definitions-qa-log.md](Topics/rosetta-stone-ai-node-definitions-qa-log.md)
(correction history, open questions, per-node Q&A notes). Content
last advanced 2026-07-17 (Checkpoints 0017-0020): node
Responsibilities/Collaborators drafted for all 9 nodes grounded in RDD
Ch. 4-5, Model's own Q&A pass completed, pseudocode-driven-comprehension
established as the working pattern, doc split into pristine reference +
Q&A log. Per the current `status` line in the reference doc: Model's
Responsibilities and Agent-as-collaborator are understood, Retrieval-
as-collaborator is flagged ambiguous, task/responsibility ownership is
still open; Agent/Tool/Retrieval/Memory/Security/Application/
Diagnostics/Deployment Context Notes have not started their own Q&A
passes. **Next up: Agent's own dedicated Q&A.**

Checkpoints 0021-0025 (2026-07-19) were cross-repo infra/cleanup —
nested-clone removal, `ai-skills` bootstrap audit, disaster-recovery
review, the `investigate` skill + unconditional Evidence Discipline,
and (0025) this Active Thread mechanism itself — and did not touch
this thread; carried forward unchanged by each.

This section is the durable "what to resume" pointer, maintained by
`update-context` on every checkpoint and read first by `lets-code` —
kept separate from "Latest checkpoint" below, which just names the
most recent session chronologically and may be infra-only.

## Topics

- [collaborative-momentum-mode](Topics/collaborative-momentum-mode.md) — current operating mode: no more freeze/phase-gating, Standards kept as reference not constraint, momentum toward real vs-mcp-bridge development (active, adopted 2026-07-14)
- [rosetta-stone-ai-node-definitions](Topics/rosetta-stone-ai-node-definitions.md) — pristine reference: Stereotype/Responsibilities/Collaborators for all 9 nodes, kept clean to study from (Q&A in progress 2026-07-17, Model underway)
- [rosetta-stone-ai-node-definitions-qa-log](Topics/rosetta-stone-ai-node-definitions-qa-log.md) — companion to the above: correction history, open questions, missing-node assessment, per-node Q&A notes — split out 2026-07-17 to keep the reference doc pristine
- [bduf-freeze-and-training](Topics/bduf-freeze-and-training.md) — superseded 2026-07-14; kept for history — the original freeze rationale and 5 pre-loaded risk findings are still real context, just no longer a gate
- [delivery-roadmap](Topics/delivery-roadmap.md) — Bill's draft roadmap from standards-foundation to sprint-based delivery: code audit of existing ChatGPT/Codex work -> gap analysis/backlog -> strict-scope sprints; the "gated on full comprehension" precondition is lifted per collaborative-momentum-mode (draft)
- [pseudocode-driven-comprehension](Topics/pseudocode-driven-comprehension.md) — working pattern for node Q&A: Bill writes pseudocode himself, Claude reviews with real rigor, the corrected block is both the comprehension check and the note (active, adopted 2026-07-17)
- [claude-in-chrome-connectivity](Topics/claude-in-chrome-connectivity.md) — recurring per-session Claude-in-Chrome domain-lockout bug and the standing workaround (open, no permanent fix)
- [xmind-copilot-collaboration](Topics/xmind-copilot-collaboration.md) — reliable methods for both editing an existing XMind map (branch-scoped Copilot batches) and building a new one from scratch (clipboard paste over simulated typing, confirmed 2026-07-13 across 4+ surfaces); known-unreliable UI patterns and a repo-diff recovery-verification method (established, reusable, with caveats)
- [architecture-artifacts-taxonomy](Topics/architecture-artifacts-taxonomy.md) — superseded; kept for incident history only — see `Architecture/rosetta-stone-AI-Architecture/` for the live document

## History

Content reset on 2026-07-12 (commit `f7269bc`, "Reset stale content
and align local workflow files"): all prior Topic files, Session
checkpoints, and Evidence stubs were deleted as part of aligning this
repo with the shared, repo-agnostic skill workflow (see `AGENTS.md`).

Latest checkpoint: [Sessions/2026-07-19_Checkpoint_0025_Active_Thread_Resume_Pointer_Added.txt](Sessions/2026-07-19_Checkpoint_0025_Active_Thread_Resume_Pointer_Added.txt)
— added a durable **Active Thread** section to this file (above) so
`lets-code` always knows the real content thread to resume, independent
of whichever checkpoint is chronologically latest; prompted by Bill
noticing that Checkpoints 0021-0024's infra/cleanup run had made
resuming ambiguous. Also settled, at Bill's prompting, that a single
global cross-repo pointer is feasible but not worth building yet — the
per-repo Active Thread plus the existing repo-picker prompt at session
start is the kept design.

Previous checkpoint: [Sessions/2026-07-19_Checkpoint_0024_Investigate_Skill_And_Evidence_Discipline.txt](Sessions/2026-07-19_Checkpoint_0024_Investigate_Skill_And_Evidence_Discipline.txt)
— added a new `investigate` skill and an unconditional "Evidence
Discipline" rule (no trigger phrase required) to every repo's
`AGENTS.md`, after Bill described a real incident where an AI assistant
stated an unverified hypothesis as fact during regulated-industry bug
triage. Extends `Standards/source-of-truth.md`'s basis vocabulary
(`authoritative`/`primary-source`/`claude-reasoning`/`unverified`)
beyond formal artifacts to every claim in every conversation, across
`architecture-rosetta-stone`, `vs-mcp-bridge`, `BlogAI`, and
`ai-skills`.

Previous checkpoint: [Sessions/2026-07-19_Checkpoint_0023_System_Wide_Review.txt](Sessions/2026-07-19_Checkpoint_0023_System_Wide_Review.txt)
— cross-repo disaster-recovery review under Bill's standing "apply best
practices without waiting for input" authorization. Found and fixed a
real bug: `sync-skills` restores by per-repo namespace, not a shared
bucket, and only the workspace root's namespace existed — a restore
from inside any of the three project repos would have silently failed.

Previous checkpoint: [Sessions/2026-07-19_Checkpoint_0022_AiSkills_Bootstrap_Audit.txt](Sessions/2026-07-19_Checkpoint_0022_AiSkills_Bootstrap_Audit.txt)
— audited whether `ai-skills` (the private GitHub skills backup) could
actually bootstrap a genuinely fresh Windows/macOS machine. Found and
fixed a circular restore instruction, a missing location map, real
local drift at the workspace root, and two repo-name typos.

Previous checkpoint: [Sessions/2026-07-19_Checkpoint_0021_Nested_Clone_Removed.txt](Sessions/2026-07-19_Checkpoint_0021_Nested_Clone_Removed.txt)
— removed a stale, fully-superseded nested clone of this same repo
(`architecture-rosetta-stone/architecture-rosetta-stone/`) after
confirming nothing but a gitignored `rdd.pdf` was at risk; relocated
that PDF to `Artifacts/XMind/rdd.pdf` directly.

Previous checkpoint: [Sessions/2026-07-17_Checkpoint_0020_Pristine_Doc_Split.txt](Sessions/2026-07-17_Checkpoint_0020_Pristine_Doc_Split.txt)
— end-of-day housekeeping: split `rosetta-stone-ai-node-definitions.md`
into a pristine reference document and a companion Q&A/discovery log
(`rosetta-stone-ai-node-definitions-qa-log.md`), so the document Bill
studies from stays clean while nothing is lost.

## Reference

- Standards: [Standards/](Standards/README.md) — cross-project rules,
  not scoped to `rosetta-stone-AI`: the `TYPE_SCOPE_SEQ` unique
  identifier scheme, a relationship-recording convention designed so a
  future triple-store/SPARQL migration (Bill's stated long-term vision,
  explicitly deep backlog) can be additive, a source-of-truth rule
  (every artifact declares whether it's `authoritative`,
  `primary-source`, or explicitly-labeled `claude-reasoning` — Bill's
  own statements are never sufficient basis alone), and a glossary — WDNA
  / Windows DNA (the three-tier reference architecture guiding component
  placement), MSF (checked against WDNA 2026-07-13, not adopted), RDD
  (Responsibility-Driven Design, the methodology `rosetta-stone-AI`
  already uses, confirmed 2026-07-14 against Bill's own copy of the
  source book — untracked in git, see the glossary entry), and AI (a
  grounded definition citing NIST's AI RMF, applied to this project's
  map structure via RDD's confederation concept).
- Architecture deliverables: [Architecture/rosetta-stone-AI-Architecture/](Architecture/rosetta-stone-AI-Architecture/README.md)
  — the living, MSDN-style BDUF artifact container companion to
  `rosetta-stone-AI` (see naming convention below). Markdown in this
  repo, not XMind — deliberately chosen 2026-07-12 over both a flat
  XMind map (scalability risk) and a GitHub wiki (would fragment git
  history into a second repo). One file per MSDN category
  (Requirements & Use Cases, Logical Architecture, Physical & Technical
  Specs, System Policies, Operational Plans), plus a 6th cross-cutting
  `risks-and-open-issues.md`. Most artifact types are still placeholder
  summaries pending `rosetta-stone-AI` Phase 1 sign-off, but Requirement
  Definitions, all 5 Risks/Known Issues, and — as of 2026-07-13 — a new
  Credential Indirection and Secure Secret Management Service
  (`SCM_RSAI_0001` + `SEC_RSAI_0001`, placed via WDNA's Business
  Services tier, contributed by Bill) are real content. Naming
  convention going forward: `rosetta-stone-<Concern>-Architecture`,
  sibling folders under `Architecture/` — next expected is
  `rosetta-stone-MCP-Bridge-Architecture` once gap-analysis work starts
  toward `vs-mcp-bridge`.
- Evidence sources: none currently populated (`Evidence/` was removed
  in the 2026-07-12 reset; recreate per-author folders here if/when
  evidence-backed work resumes)
- Mindmap: four active XMind Cloud documents, none frozen as of
  2026-07-14 (see `Topics/collaborative-momentum-mode.md`) —
  `rosetta-stone-AI` (the Responsibility vocabulary,
  https://app.xmind.com/GPJHh8wQ), `rosetta-stone-MCP-Bridge` (the
  split-out MCP IDE-extension delivery concern,
  https://app.xmind.com/IPtIA0Kd), `rosetta-stone-WDNA-Reference`
  (https://app.xmind.com/7oUcRnoy, built 2026-07-13, a WDNA
  teaching/reference map — see `Standards/glossary.md`'s WDNA entry),
  and `MCP AI Components CRC Card Analysis`
  (https://app.xmind.com/vZP5O1WP, built 2026-07-14 in ~5 minutes via a
  single prompt — a 7-node CRC model of Application/Model/Agent/Tool/
  Retrieval/Memory/Security that's the current working draft for
  defining those terms; mirrored at
  `Artifacts/XMind/mcp-ai-components-crc-card-analysis.txt`). Edited via
  Claude-in-Chrome + XMind Copilot (see
  `Topics/xmind-copilot-collaboration.md`). Point-in-time snapshots of
  `rosetta-stone-AI` and `rosetta-stone-MCP-Bridge` as they stood at the
  2026-07-12 split (`.xmind` source + `.outline.md` readable mirror) are
  committed under `Artifacts/XMind/` for history — no longer enforced as
  the only allowed state now that the freeze is lifted.
  `Artifacts/XMind/` also holds incident writeups and per-session
  Chrome-permission fix scripts (see
  `Topics/claude-in-chrome-connectivity.md`) — a fresh `.command` script
  is generated each session, so treat any existing one there as
  possibly stale.
- Related repos (context only, not actively worked on):
  `/Users/billkratochvil/AI/repos/vs-mcp-bridge`,
  `/Users/billkratochvil/AI/repos/BlogAI`
