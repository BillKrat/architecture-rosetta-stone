---
name: bduf-freeze-and-training
description: The BDUF (Big Design Up Front) working agreement for this project — the two frozen source-of-truth maps, and the training-before-touching protocol now in effect.
status: superseded 2026-07-14 — the freeze and phase-gating described below are lifted; kept for history only. See Topics/collaborative-momentum-mode.md for current state.
last-updated: 2026-07-14
---

## SUPERSEDED 2026-07-14 — read collaborative-momentum-mode.md first

Everything below this notice is historical record, not current working
agreement. After four days with zero progress on the actual objective
(Bill's comprehension, unblocking real `vs-mcp-bridge` development) —
the Application node's three opening questions were never answered —
Bill removed the content freeze and the phase-gating described here.
See `Topics/collaborative-momentum-mode.md` for what replaced it, and
why. The reasoning captured below (why BDUF, the freeze rationale, the
5 pre-loaded risk findings) is still real and still useful context; it's
just no longer a gate anything has to wait behind.

## Why BDUF here

There is no existing documentation and no product owner who can supply the
design — the vocabulary itself has to be worked out from first principles.
Bill's chosen approach is Big Design Up Front: freeze a complete draft,
build comprehensive shared understanding of it, then deliberately
investigate/tear down/rebuild from that common footing — rather than
iterating on a moving target.

## The freeze

On 2026-07-12, after the bullet-prefix cleanup (see
`Topics/xmind-copilot-collaboration.md`) surfaced that the `rosetta-stone-AI`
XMind Cloud document actually mixed two unrelated concerns, it was split
into two documents, each frozen as source of truth:

- **`rosetta-stone-AI`** (https://app.xmind.com/GPJHh8wQ) — Concern A, the
  actual Rosetta Stone content: the AI-system Responsibility vocabulary.
  Branches: Application, Model (+ API-service/Edge/RAG variants), Agent,
  Tool, Retrieval, Memory, Security, Deployment Context Notes,
  Cross-cutting fields template, Diagnostics/Observability.
- **`rosetta-stone-MCP-Bridge`** (https://app.xmind.com/IPtIA0Kd) —
  Concern B, a distinct implementation concern: the delivery architecture
  for an MCP-based IDE extension/host-bridge tool (reads like the
  `vs-mcp-bridge` repo's design, not general AI vocabulary). Branches:
  Transport (MCP/stdio/named-pipe), Host (VSIX/IDE), Testing/CI,
  Packaging/Release, Connector/Adapter.

Both were produced by duplicating the original document, then pruning each
copy down to only its own concern (see git history for the exact prune
steps). Each was verified clean (no stray bullet-dot title prefixes, no
cross-concern content) via a full outline reload-and-read after the split.

Frozen snapshots of both are committed to this repo as the permanent
record:
- `Artifacts/XMind/rosetta-stone-AI.xmind` +
  `Artifacts/XMind/rosetta-stone-AI.outline.md` (readable mirror)
- `Artifacts/XMind/rosetta-stone-MCP-Bridge.xmind` +
  `Artifacts/XMind/rosetta-stone-MCP-Bridge.outline.md` (readable mirror)

The `.xmind` files are the source of record; the `.outline.md` files exist
purely so the frozen content is diffable/readable directly in git without
opening XMind.

## The working agreement now in effect

**No modification and no investigation of either frozen map** until Bill
has built a comprehensive understanding of every node — every
Responsibility and every Collaborator relationship represented in
`rosetta-stone-AI` specifically (the actual project content; the
MCP-Bridge document is a parked, unrelated concern for now).

Once that shared understanding exists, the plan is: investigate the design
together, tear down what doesn't hold up, build up what's missing, and
converge on a final `rosetta-stone-AI` that's solid enough to start real
development from.

**Session scope, tightened 2026-07-13 (Bill's own words):** the
"Coding Session" is *only* this — mentoring/education on the two frozen
maps, `rosetta-stone-AI` first, then `rosetta-stone-MCP-Bridge` once
Concern A is signed off (Phase 3 below). "No other conversations are
meant to take place in there... No coding, no updates." If an idea,
process, or standard surfaces during a walkthrough, that session's job
is to route it into the right Standards/Architecture location and
update context to reflect the routing — not to develop it there. See
`Topics/delivery-roadmap.md` for where the routed-to work (standards,
gap analysis, backlog, sprints) actually happens, and why it's
deliberately a different session.

## Training scope (defined 2026-07-12)

**Every training conversation must stay strictly within the nodes of the
frozen `rosetta-stone-AI` map — the whole of each node, and nothing
outside it.**

"The whole of each node" means all fields the map actually carries per
node, not a reduced subset:
Responsibilities, Collaborators, Inputs/Outputs, Metrics & Thresholds,
Known Failure Modes, Runtime Hooks, Regulatory Notes, Owner, Acceptance
Criteria — across all 10 top-level branches (Application, Model, Agent,
Tool, Retrieval, Memory, Security, Deployment Context Notes, Cross-cutting
fields, Diagnostics/Observability) plus Model's 3 deployment variants
(API-service / Edge / RAG).

This was clarified after Bill proposed a car-analogy conceptual model
("AI Car Conceptual Model — Responsibility-Driven Design") as a
scope-check: an implementation-agnostic frame using only Responsibilities
+ Collaborations, explicitly excluding vendor/technology differences
(Copilot vs. ChatGPT vs. Claude vs. Google AI mode = "engine type," same
non-issue as gas vs. diesel vs. electric). The analogy itself was
confirmed as a correct instance of the RDD principle already embedded in
the map (see `Deployment Context Notes`, which treats
API-service/Edge/RAG the same way — deployment variants, not different
Models). But Bill then clarified the actual scope decision: he wants
**everything on the diagram**, not the reduced Responsibilities+
Collaborations-only slice the car analogy modeled — because he doesn't
yet know what he doesn't know, so narrowing the field set in advance
risks leaving gaps. The car analogy's job was to validate that Claude and
Bill share the same RDD frame; it is not itself an ongoing simplification
of the training curriculum.

**Explicitly out of scope for these conversations:**
- `rosetta-stone-MCP-Bridge` (the other frozen document — parked,
  unrelated concern)
- Any content, comparison, or tangent not represented by a node in
  `rosetta-stone-AI` (e.g. specific AI product/vendor discussion beyond
  what's needed to confirm a Responsibility is vendor-agnostic)

**Rationale:** Bill's stated assumption is that full node-by-node
comprehension is what lets him engage with Claude's questions
intelligently going forward, establishing the common foundational
understanding the later investigate/tear-down/rebuild phase depends on.
Staying strictly inside the map's nodes is what makes that foundation
actually common — scope creep into adjacent topics would undermine the
premise.

## Full roadmap (defined 2026-07-12)

Five phases, each gated on the previous one's completion:

1. **Train on Concern A (`rosetta-stone-AI`), node-by-node.** Order is
   clockwise from the map's current layout: Application -> Model (incl.
   API-service/Edge/RAG variants) -> Agent -> Tool -> Retrieval -> Memory
   -> Security -> Deployment Context Notes -> Cross-cutting fields ->
   Diagnostics/Observability. Per node: Claude asks questions covering
   every field (Responsibilities, Collaborators, Inputs/Outputs, Metrics
   & Thresholds, Known Failure Modes, Runtime Hooks, Regulatory Notes,
   Owner, Acceptance Criteria — see Training Scope above), Bill answers
   and works through them, Claude judges when understanding is solid.
   When both agree a node is understood, its task-checkbox on the live
   `rosetta-stone-AI` map is checked off and the walkthrough moves to
   the next node. **Checking these checkboxes is the one sanctioned
   exception to the "no modification" freeze** — it's status tracking,
   not content editing; no Responsibility/Collaborator/field text
   changes during this phase.
2. **Unfreeze and jointly re-investigate Concern A.** Once every
   checkbox from Phase 1 is checked, uncheck all of them, lift the
   content freeze, and go through the map again — this time
   investigating, discussing, and mutually agreeing on each node's
   actual correctness (not just comprehension). Nodes may be added,
   expanded, or contracted as warranted. Check off each node's box again
   as Bill and Claude both sign off on it.
3. **Repeat phases 1-2 on Concern B (`rosetta-stone-MCP-Bridge`).** Same
   train-then-investigate structure, applied to the parked MCP
   IDE-extension delivery document once Concern A is fully signed off.
4. **Gap analysis.** Once both documents are signed off, assess current
   state (what the two finalized maps represent) versus target state
   (what's actually needed) to identify what's missing or wrong.
5. **Requirements document and backlog.** Convert the gap analysis into
   concrete requirements and a working backlog — the actual handoff into
   development.

## Phase 1 progress

- **Node 1/10 — Application: IN PROGRESS, not yet checked off.** Claude
  opened the walkthrough with three questions: (1) what is Application's
  unique Responsibility that no other node could take over, (2) which
  other nodes does Application collaborate with and why, (3) where's the
  boundary between Application and Model — if a user sees a wrong or
  misleading answer, whose fault is it and how do you tell? Bill has not
  yet answered these; session ended before working through them. **This
  is the exact resume point for the next session** — do not restart the
  Application walkthrough from scratch or re-ask different opening
  questions; pick up with these same three.
- Nodes 2-10 (Model, Agent, Tool, Retrieval, Memory, Security, Deployment
  Context Notes, Cross-cutting fields, Diagnostics/Observability): not
  started.

## Known findings from a parallel session (2026-07-12) — read before resuming Phase 1

A same-day, parallel Claude Code session (BDUF-research, not this
Phase 1 training track) ran a collaborator-relationship diagram and an
ownership audit against this frozen map, looking for violations of "every
Responsibility should have exactly one owner." **No edits were made to
`rosetta-stone-AI`** — the freeze held — but 5 findings were formalized
as tracked Risks/Known Issues in
`Architecture/rosetta-stone-AI-Architecture/risks-and-open-issues.md`
(`RSK_RSAI_0001` through `0005`), against two new Requirement
Definitions in `Architecture/rosetta-stone-AI-Architecture/requirements-and-use-cases.md`
(`RD_RSAI_0001`, `RD_RSAI_0002`). Summary, one line each:

- `RSK_RSAI_0001` — Diagnostics/Observability has no `Owner:` field at all.
- `RSK_RSAI_0002` — Deployment-context (API-service/Edge/RAG) responsibilities are modeled twice, under two different owners.
- `RSK_RSAI_0003` — Provenance/grounding is independently claimed by Retrieval, Model (RAG), and Deployment Context Notes.
- `RSK_RSAI_0004` — PII/data-handling policy is split three ways across Security, Memory, and Tool with no stated precedence.
- `RSK_RSAI_0005` — Takedown/DMCA handling is worded near-identically in both Retrieval and Model (RAG).

**Why this doesn't conflict with the freeze:** the working agreement above
prohibits *modifying or investigating the frozen map's content*. What
happened is upstream of that — a diagram and an audit *of* the map, with
findings recorded in the separate, unfrozen `Architecture/` document, not
written back into `rosetta-stone-AI` itself. Whether each finding is a
real defect to fix when Phase 1 training reaches its node, or a
conscious "actually fine as-is" call, is exactly the kind of judgment
Phase 1/Phase 2 exists to make — nothing here presumes the answer. Bill
directed this be captured for continuity ("this will help the other
session as well as Claude mentors, educates, and ramps me up") rather
than left buried in a checkpoint only the BDUF-research session would
read again.

This resolves Checkpoint 0006's "Flag for Bill" (the concern that
investigating the frozen map without this agreement in context might
have been out of scope) — Bill confirmed the investigation's *output*
is welcome specifically because it landed here, as tracked findings, not
as edits.

## Open questions

- None currently — scope and roadmap are both settled as of 2026-07-12.
  Training format is the roadmap itself; no separate format decision
  remains open. Execution is mid-flight (see Phase 1 progress above).
  When Phase 1 reaches nodes Diagnostics/Observability, Deployment
  Context Notes, Retrieval, Model, Security, Memory, or Tool, also
  resolve the corresponding finding(s) above as part of that node's
  walkthrough rather than treating them as a separate pass.
