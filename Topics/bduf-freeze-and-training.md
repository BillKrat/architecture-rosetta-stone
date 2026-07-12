---
name: bduf-freeze-and-training
description: The BDUF (Big Design Up Front) working agreement for this project — the two frozen source-of-truth maps, and the training-before-touching protocol now in effect.
status: active — frozen maps in place, training scope defined, format not yet started
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

## Open questions

- What does the training phase look like mechanically (session
  structure, whether Claude proctors/quizzes, whether it's self-paced
  reading)? Scope is now settled; format/cadence is not.
- `rosetta-stone-MCP-Bridge` has no defined next step yet — it's frozen and
  parked, not part of the training curriculum.
