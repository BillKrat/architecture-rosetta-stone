# Rosetta Stone for Software Architecture — Index

Establish a shared, tested vocabulary for AI system architecture —
where every term names a distinct Responsibility, not an overloaded or
borrowed one — so architects can build and discuss these systems
without inheriting meaning-drift. AI is the current test case running
through the method, not the boundary of it.

**Binding standards — read before authoring anything, in any session:**
this project's terminology source of truth for architectural layers is
**WDNA (Windows DNA)** — Presentation / Business / Data Services — not
ad hoc naming. Every architecture *document* this project produces
follows the templates in `Standards/document-layout.md`; every tracked
*artifact* gets an ID per `Standards/identifier-scheme.md`, declares its
`basis` per `Standards/source-of-truth.md`, and records cross-references
per `Standards/relationship-vocabulary.md`. This applies identically
whether you're in this BDUF-research thread or the Phase 1
training/"coding session" thread — see `Standards/README.md` for the
full set. Established 2026-07-12/13; not optional polish (see that
folder's own "why this exists" for why).

**This file is a map, not content.** It holds one line per topic and a
link — the actual state lives in `Topics/`. Read this in full; open a
`Topics/*.md` file only when that topic is relevant to what you're
doing.

## Topics

- [bduf-freeze-and-training](Topics/bduf-freeze-and-training.md) — frozen maps + the full 5-phase BDUF roadmap; Phase 1 mid-walkthrough on node 1/10 (Application) — resume point recorded (active); now includes a "known findings from a parallel session" pointer for 5 pre-loaded risks the coding session should use when it reaches the relevant nodes; Coding Session scope tightened 2026-07-13 (mentoring only, no coding/updates there)
- [delivery-roadmap](Topics/delivery-roadmap.md) — Bill's draft (not committed) roadmap from standards-foundation to sprint-based delivery: code audit of existing ChatGPT/Codex work -> gap analysis/backlog -> strict-scope sprints, gated on Bill's full comprehension of both maps + standards (draft)
- [claude-in-chrome-connectivity](Topics/claude-in-chrome-connectivity.md) — recurring per-session Claude-in-Chrome domain-lockout bug and the standing workaround (open, no permanent fix)
- [xmind-copilot-collaboration](Topics/xmind-copilot-collaboration.md) — reliable methods for both editing an existing XMind map (branch-scoped Copilot batches) and building a new one from scratch (clipboard paste over simulated typing, confirmed 2026-07-13 across 4+ surfaces); known-unreliable UI patterns and a repo-diff recovery-verification method (established, reusable, with caveats)
- [architecture-artifacts-taxonomy](Topics/architecture-artifacts-taxonomy.md) — superseded; kept for incident history only — see `Architecture/rosetta-stone-AI-Architecture/` for the live document

## History

Content reset on 2026-07-12 (commit `f7269bc`, "Reset stale content
and align local workflow files"): all prior Topic files, Session
checkpoints, and Evidence stubs were deleted as part of aligning this
repo with the shared, repo-agnostic skill workflow (see `AGENTS.md`).

Latest checkpoint: [Sessions/2026-07-13_Checkpoint_0013_WDNA_Reference_Map_And_Demo.txt](Sessions/2026-07-13_Checkpoint_0013_WDNA_Reference_Map_And_Demo.txt)
— built `rosetta-stone-WDNA-Reference` (https://app.xmind.com/7oUcRnoy),
closing Checkpoint 0009's deferred task, while it doubled as a live,
recorded demo for Bill's work team (active company Claude evaluation
context). Recovered from two real incidents on camera (a stray-node
mishap solved by starting fresh; a full accidental deletion solved by
having Copilot rebuild the whole structure from one fully-specified
prompt). Two UI reliability fixes came directly from Bill and are now
confirmed and folded into `Topics/xmind-copilot-collaboration.md`:
paste a dash-bulleted list onto a selected node to create children
reliably, and paste (not type) into any XMind text field to avoid a
word-order-scrambling bug. Phase 1 training and the delivery-roadmap
gate remain untouched.

## Reference

- Standards: [Standards/](Standards/README.md) — cross-project rules,
  not scoped to `rosetta-stone-AI`: the `TYPE_SCOPE_SEQ` unique
  identifier scheme, a relationship-recording convention designed so a
  future triple-store/SPARQL migration (Bill's stated long-term vision,
  explicitly deep backlog) can be additive, a source-of-truth rule
  (every artifact declares whether it's `authoritative`,
  `primary-source`, or explicitly-labeled `claude-reasoning` — Bill's
  own statements are never sufficient basis alone), and a glossary (WDNA
  / Windows DNA, the three-tier reference architecture now guiding
  component placement; and MSF / Microsoft Solutions Framework, checked
  against WDNA 2026-07-13 and explicitly not adopted).
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
- Mindmap: three active XMind Cloud documents. Two frozen as of
  2026-07-12 — `rosetta-stone-AI` (the Responsibility vocabulary,
  https://app.xmind.com/GPJHh8wQ) and `rosetta-stone-MCP-Bridge` (the
  split-out MCP IDE-extension delivery concern,
  https://app.xmind.com/IPtIA0Kd). A third, `rosetta-stone-WDNA-Reference`
  (https://app.xmind.com/7oUcRnoy, built 2026-07-13), is a living WDNA
  teaching/reference map — see `Standards/glossary.md`'s WDNA entry, not
  frozen. Edited via Claude-in-Chrome + XMind Copilot (see
  `Topics/xmind-copilot-collaboration.md`, which now covers both
  editing an existing map and building a new one). Frozen snapshots of
  the two Concern documents (`.xmind` source + `.outline.md` readable
  mirror) are committed under `Artifacts/XMind/` — see
  `Topics/bduf-freeze-and-training.md` for the freeze rationale and the
  standing working agreement (the WDNA reference map is not part of
  that freeze). `Artifacts/XMind/` also holds incident writeups and
  per-session Chrome-permission fix scripts (see
  `Topics/claude-in-chrome-connectivity.md`) — a fresh `.command`
  script is generated each session, so treat any existing one there as
  possibly stale.
- Related repos (context only, not actively worked on):
  `/Users/billkratochvil/AI/repos/vs-mcp-bridge`,
  `/Users/billkratochvil/AI/repos/BlogAI`
