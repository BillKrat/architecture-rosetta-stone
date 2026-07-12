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

- [bduf-freeze-and-training](Topics/bduf-freeze-and-training.md) — frozen maps + the training-before-touching working agreement; training scope is strictly the nodes of `rosetta-stone-AI` (active)
- [claude-in-chrome-connectivity](Topics/claude-in-chrome-connectivity.md) — recurring per-session Claude-in-Chrome domain-lockout bug and the standing workaround (open, no permanent fix)
- [xmind-copilot-collaboration](Topics/xmind-copilot-collaboration.md) — reliable method for bulk-editing the XMind map via its Copilot (established, reusable)

## History

Content reset on 2026-07-12 (commit `f7269bc`, "Reset stale content
and align local workflow files"): all prior Topic files, Session
checkpoints, and Evidence stubs were deleted as part of aligning this
repo with the shared, repo-agnostic skill workflow (see `AGENTS.md`).

Latest checkpoint: [Sessions/2026-07-12_Checkpoint_0003_Training_Scope_Defined.txt](Sessions/2026-07-12_Checkpoint_0003_Training_Scope_Defined.txt)
— defined the scope of the training phase established in Checkpoint 0002:
every conversation must stay strictly within the nodes of the frozen
`rosetta-stone-AI` map (all fields, all branches), and nothing outside it.
See `Topics/bduf-freeze-and-training.md`.

## Reference

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
