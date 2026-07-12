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

- [claude-in-chrome-connectivity](Topics/claude-in-chrome-connectivity.md) — recurring per-session Claude-in-Chrome domain-lockout bug and the standing workaround (open, no permanent fix)
- [xmind-copilot-collaboration](Topics/xmind-copilot-collaboration.md) — reliable method for bulk-editing the XMind map via its Copilot (established, reusable)

## History

Content reset on 2026-07-12 (commit `f7269bc`, "Reset stale content
and align local workflow files"): all prior Topic files, Session
checkpoints, and Evidence stubs were deleted as part of aligning this
repo with the shared, repo-agnostic skill workflow (see `AGENTS.md`).

Latest checkpoint: [Sessions/2026-07-12_Checkpoint_0001_XMind_Copilot_Cleanup.txt](Sessions/2026-07-12_Checkpoint_0001_XMind_Copilot_Cleanup.txt)
— first checkpoint under the current structure. Connected Claude-in-Chrome
to the `rosetta-stone-AI` XMind Cloud map, worked out a reliable
Copilot-driven bulk-edit method, and used it to strip a stray
bullet-dot-prefix formatting defect from ~122 topic titles across the
whole map, giving a clean foundational document to build the actual
architecture content on next.

## Reference

- Evidence sources: none currently populated (`Evidence/` was removed
  in the 2026-07-12 reset; recreate per-author folders here if/when
  evidence-backed work resumes)
- Mindmap: two XMind Cloud documents (`rosetta-stone-architecture`,
  `rosetta-stone-AI`), live-edited via Claude-in-Chrome + XMind Copilot
  (see `Topics/xmind-copilot-collaboration.md`). `rosetta-stone-AI` is
  the active one as of 2026-07-12. No local `.xmind` snapshots are
  kept — the cloud document is the source of truth. `Artifacts/XMind/`
  holds incident writeups and per-session Chrome-permission fix
  scripts (see `Topics/claude-in-chrome-connectivity.md`) — a fresh
  `.command` script is generated each session, so treat any existing
  one there as possibly stale.
- Related repos (context only, not actively worked on):
  `/Users/billkratochvil/AI/repos/vs-mcp-bridge`,
  `/Users/billkratochvil/AI/repos/BlogAI`
