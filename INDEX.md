# Rosetta Stone for Software Architecture — Index

Establish a shared, tested vocabulary for AI system architecture —
where every term names a distinct Responsibility, not an overloaded or
borrowed one — so architects can build and discuss these systems
without inheriting meaning-drift. AI is the current test case running
through the method, not the boundary of it.

**This file is a map, not content.** It holds one line per topic and a
link — the actual state lives in `Topics/`. Read this in full; open a
`Topics/*.md` file only when that topic is relevant to what you're
doing.

## Topics

- [bduf-freeze-and-training](Topics/bduf-freeze-and-training.md) — frozen maps + the full 5-phase BDUF roadmap; Phase 1 mid-walkthrough on node 1/10 (Application) — resume point recorded (active); now includes a "known findings from a parallel session" pointer for 5 pre-loaded risks the coding session should use when it reaches the relevant nodes
- [claude-in-chrome-connectivity](Topics/claude-in-chrome-connectivity.md) — recurring per-session Claude-in-Chrome domain-lockout bug and the standing workaround (open, no permanent fix)
- [xmind-copilot-collaboration](Topics/xmind-copilot-collaboration.md) — reliable method for bulk-editing the XMind map via its Copilot, plus known-unreliable surfaces (chat-panel click targeting, AI landing-page Enter-submit) and a repo-diff recovery-verification method (established, reusable, with caveats)
- [architecture-artifacts-taxonomy](Topics/architecture-artifacts-taxonomy.md) — superseded; kept for incident history only — see `Architecture/rosetta-stone-AI-Architecture/` for the live document

## History

Content reset on 2026-07-12 (commit `f7269bc`, "Reset stale content
and align local workflow files"): all prior Topic files, Session
checkpoints, and Evidence stubs were deleted as part of aligning this
repo with the shared, repo-agnostic skill workflow (see `AGENTS.md`).

Latest checkpoint: [Sessions/2026-07-12_Checkpoint_0007_Standards_And_Handoff.txt](Sessions/2026-07-12_Checkpoint_0007_Standards_And_Handoff.txt)
— same parallel BDUF-research session as Checkpoint 0006, closing out
for the evening. Built `Standards/` (identifier scheme + relationship
vocabulary), then exercised both for real: formalized the
single-owner-per-Responsibility principle as `RD_RSAI_0001`/`0002` and
converted Checkpoint 0006's ownership-audit findings into
`RSK_RSAI_0001`-`0005` in
`Architecture/rosetta-stone-AI-Architecture/risks-and-open-issues.md`.
Resolves Checkpoint 0006's "Flag for Bill": findings live in the
unfrozen Architecture document, never written back into the frozen map,
with a handoff pointer added to `Topics/bduf-freeze-and-training.md` for
the coding-session track. Phase 1 training itself remains untouched —
its resume point is still Checkpoint 0005's (Application, three opening
questions unanswered).

## Reference

- Standards: [Standards/](Standards/README.md) — cross-project rules,
  not scoped to `rosetta-stone-AI`: the `TYPE_SCOPE_SEQ` unique
  identifier scheme for every requirement/use-case/diagram/deliverable
  across every project, and a relationship-recording convention
  designed so a future triple-store/SPARQL migration (Bill's stated
  long-term vision, explicitly deep backlog, not current work) can be
  additive instead of a rewrite.
- Architecture deliverables: [Architecture/rosetta-stone-AI-Architecture/](Architecture/rosetta-stone-AI-Architecture/README.md)
  — the living, MSDN-style BDUF artifact container companion to
  `rosetta-stone-AI` (see naming convention below). Markdown in this
  repo, not XMind — deliberately chosen 2026-07-12 over both a flat
  XMind map (scalability risk) and a GitHub wiki (would fragment git
  history into a second repo). One file per MSDN category
  (Requirements & Use Cases, Logical Architecture, Physical & Technical
  Specs, System Policies, Operational Plans), plus a 6th cross-cutting
  `risks-and-open-issues.md`. Most artifact types are still placeholder
  summaries pending `rosetta-stone-AI` Phase 1 sign-off, but two
  Requirement Definitions and all 5 Risks/Known Issues are real content
  as of 2026-07-12 — see `Topics/bduf-freeze-and-training.md`'s "Known
  findings" section. Naming convention going forward:
  `rosetta-stone-<Concern>-Architecture`, sibling folders under
  `Architecture/` — next expected is
  `rosetta-stone-MCP-Bridge-Architecture` once gap-analysis work starts
  toward `vs-mcp-bridge`.
- Evidence sources: none currently populated (`Evidence/` was removed
  in the 2026-07-12 reset; recreate per-author folders here if/when
  evidence-backed work resumes)
- Mindmap: two active XMind Cloud documents, both frozen as of
  2026-07-12 — `rosetta-stone-AI` (the Responsibility vocabulary,
  https://app.xmind.com/GPJHh8wQ) and `rosetta-stone-MCP-Bridge` (the
  split-out MCP IDE-extension delivery concern,
  https://app.xmind.com/IPtIA0Kd). Edited via Claude-in-Chrome + XMind
  Copilot (see `Topics/xmind-copilot-collaboration.md`). Frozen
  snapshots of both (`.xmind` source + `.outline.md` readable mirror)
  are committed under `Artifacts/XMind/` — see
  `Topics/bduf-freeze-and-training.md` for the freeze rationale and the
  standing working agreement. `Artifacts/XMind/` also holds incident
  writeups and per-session Chrome-permission fix scripts (see
  `Topics/claude-in-chrome-connectivity.md`) — a fresh `.command`
  script is generated each session, so treat any existing one there as
  possibly stale.
- Related repos (context only, not actively worked on):
  `/Users/billkratochvil/AI/repos/vs-mcp-bridge`,
  `/Users/billkratochvil/AI/repos/BlogAI`
