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

## Topics

- [collaborative-momentum-mode](Topics/collaborative-momentum-mode.md) — current operating mode: no more freeze/phase-gating, Standards kept as reference not constraint, momentum toward real vs-mcp-bridge development (active, adopted 2026-07-14)
- [rosetta-stone-ai-node-definitions](Topics/rosetta-stone-ai-node-definitions.md) — queued: flesh out Responsibilities/Collaborators for Model, Agent, Tool, Retrieval, Memory, Security, Application, Diagnostics/Observability, Deployment Context Notes, plus a check for missing nodes (assigned 2026-07-16, not started)
- [bduf-freeze-and-training](Topics/bduf-freeze-and-training.md) — superseded 2026-07-14; kept for history — the original freeze rationale and 5 pre-loaded risk findings are still real context, just no longer a gate
- [delivery-roadmap](Topics/delivery-roadmap.md) — Bill's draft roadmap from standards-foundation to sprint-based delivery: code audit of existing ChatGPT/Codex work -> gap analysis/backlog -> strict-scope sprints; the "gated on full comprehension" precondition is lifted per collaborative-momentum-mode (draft)
- [claude-in-chrome-connectivity](Topics/claude-in-chrome-connectivity.md) — recurring per-session Claude-in-Chrome domain-lockout bug and the standing workaround (open, no permanent fix)
- [xmind-copilot-collaboration](Topics/xmind-copilot-collaboration.md) — reliable methods for both editing an existing XMind map (branch-scoped Copilot batches) and building a new one from scratch (clipboard paste over simulated typing, confirmed 2026-07-13 across 4+ surfaces); known-unreliable UI patterns and a repo-diff recovery-verification method (established, reusable, with caveats)
- [architecture-artifacts-taxonomy](Topics/architecture-artifacts-taxonomy.md) — superseded; kept for incident history only — see `Architecture/rosetta-stone-AI-Architecture/` for the live document

## History

Content reset on 2026-07-12 (commit `f7269bc`, "Reset stale content
and align local workflow files"): all prior Topic files, Session
checkpoints, and Evidence stubs were deleted as part of aligning this
repo with the shared, repo-agnostic skill workflow (see `AGENTS.md`).

Latest checkpoint: [Sessions/2026-07-16_Checkpoint_0016_AI_Definition_Applied_And_Node_Work_Queued.txt](Sessions/2026-07-16_Checkpoint_0016_AI_Definition_Applied_And_Node_Work_Queued.txt)
— the `AI` glossary entry's grounded content was applied outside this
repo for the first time (a `vs-mcp-bridge` blog post), and Bill queued
the next real work: flesh out Responsibilities/Collaborators for
`rosetta-stone-AI`'s 9 core nodes, see
`Topics/rosetta-stone-ai-node-definitions.md`.

Previous checkpoint: [Sessions/2026-07-14_Checkpoint_0015_First_Grounded_AI_Definition.txt](Sessions/2026-07-14_Checkpoint_0015_First_Grounded_AI_Definition.txt)
— first real content under the new mode: read `rdd.pdf` (Bill's RDD
book, partial scan) and verified NIST's AI RMF definition of "AI
system" directly from source, then wrote grounded `RDD` and `AI`
entries in `Standards/glossary.md`. Caught and fixed a copyright
over-quoting issue before it reached git.

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
