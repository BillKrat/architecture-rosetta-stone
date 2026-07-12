---
name: bduf-freeze-and-training
description: The BDUF (Big Design Up Front) working agreement for this project — the two frozen source-of-truth maps, and the training-before-touching protocol now in effect.
status: active — Phase 1 in progress, mid-walkthrough on node 1/10 (Application)
last-updated: 2026-07-12
---

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

## Open questions

- None currently — scope and roadmap are both settled as of 2026-07-12.
  Training format is the roadmap itself; no separate format decision
  remains open. Execution is mid-flight (see Phase 1 progress above).
