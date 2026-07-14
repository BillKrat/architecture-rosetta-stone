---
name: delivery-roadmap
description: Bill's draft roadmap from BDUF-standards-foundation through to sprint-based delivery of vs-mcp-bridge — explicitly not committed, "a roadmap, not thee roadmap," decided together.
status: draft — Bill's leaning, open for joint revision; nothing on it has started
last-updated: 2026-07-13
---

## Status, stated plainly

Bill's own framing (2026-07-13): "not 'thee' roadmap, just one I am
leaning into - 'we' can decide the roadmap together... This isn't set
in stone and we don't have to solve and commit to anything right now."
Recorded here so it isn't lost between sessions, not because it's been
adopted as binding. Treat as a strong draft, revisit before treating any
step as started.

## Session roles this roadmap depends on

See `Topics/bduf-freeze-and-training.md`'s "Session scope, tightened
2026-07-13" for the authoritative version — summarized here for context:

- **Coding Session** — mentoring/education only, on the two frozen maps
  in order (`rosetta-stone-AI`, then `rosetta-stone-MCP-Bridge`). No
  other work happens there; ideas get routed elsewhere, not developed
  in place.
- **This session (labeled "UML Diagram app integration")** — where
  standards get formalized "for us and any future contributors."
  Outside contribution explicitly discouraged until the app reaches at
  least a beta with a solid foundation in place.

## WDNA learning goal, recalibrated

Bill: familiarity with WDNA is enough — he doesn't need mastery, because
"the standards will drive the usage of it," not raw WDNA knowledge on
its own. Lowers the bar on the WDNA reference-map task
(`Sessions/2026-07-13_Checkpoint_0009_*.txt`, "Deferred") somewhat —
still useful, not a comprehension gate on its own.

## The gate

Everything below waits on Bill reaching **full comprehension**: both
frozen maps understood (Coding Session, Phases 1-3 in
`bduf-freeze-and-training.md`), and familiarity with this project's own
Standards. Not gated on this session's work being "done" — Standards
keep evolving; the gate is Bill's comprehension level, not a finish
line on the documents themselves.

## Then: three steps, in strict order

1. **Full analysis of the existing ChatGPT/Codex-generated code.** Bill
   has prior AI-generated code for `vs-mcp-bridge` already (source:
   ChatGPT / Codex, predates this project's current process). Claude
   analyzes it for risks, what works, what doesn't, what remains.
   Location not yet specified — likely somewhere under the
   `vs-mcp-bridge` repo (see root `INDEX.md`'s "Related repos"), to be
   confirmed when this step actually starts.
2. **Gap analysis and prioritized backlog.** Claude produces a gap
   analysis (current state vs. target) and a prioritized backlog of
   PBIs (Product Backlog Items) needed to reach a beta.
3. **Sprint cycles, strict scope discipline.** Work only the PBIs
   assigned to the current sprint. Reprioritization sends something back
   to the backlog rather than being worked ad hoc alongside the sprint's
   actual scope.

This is a deliberate two-phase split, not a contradiction with the
project's BDUF approach elsewhere: BDUF rigor for the
architecture/standards foundation (justified by real stakes — see
`Architecture/rosetta-stone-AI-Architecture/risks-and-open-issues.md`'s
`RSK_RSAI_0006`), Agile/Scrum sprint discipline once that foundation is
solid enough to build from. Notably, Agile is the same shift that
obsoleted Bill's own MCSD certification track (see
`Standards/glossary.md`'s MSF entry) — not rejected here, deliberately
sequenced to where it's actually the right tool.

## Open items, not blocking, for whenever this roadmap gets picked up again

- Where the ChatGPT/Codex code actually lives.
- "Code reviews by you will protect us" (Bill, re: future code work) —
  worth calibrating explicitly when it comes up: real risk reduction,
  not a guarantee, especially given `RSK_RSAI_0006`'s stakes. Whether
  additional safeguards (automated testing, external security review
  before a real beta release) belong in "beta-ready" alongside code
  review is worth raising, not decided.
