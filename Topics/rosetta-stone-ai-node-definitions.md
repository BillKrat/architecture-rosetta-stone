---
name: rosetta-stone-ai-node-definitions
description: Queued work — flesh out Responsibilities and Collaborators for rosetta-stone-AI's core nodes (Model, Agent, Tool, Retrieval, Memory, Security, Application, Diagnostics/Observability, Deployment Context Notes), grounded per collaborative-momentum-mode's method, plus an explicit check for missing nodes.
status: queued — assigned 2026-07-16, not started
last-updated: 2026-07-16
---

## What this is

Bill's next assignment (2026-07-16), verbatim scope — flesh out the
Responsibilities and Collaborators (the two RDD fields
`rosetta-stone-AI` already uses per node, see `Standards/glossary.md`'s
`RDD` entry) for each of the following, and assess whether any other
nodes belong alongside them:

- **Model** — the learned, probabilistic reasoning/generation core. The
  one component whose behavior genuinely comes from training, not code.
- **Agent** — decomposes goals, sequences steps, decides which Tool or
  Model call happens next. Gives the confederation direction.
- **Tool** — deterministic, narrowly-scoped execution the Model can't do
  reliably itself (math, code execution, live lookups). Where
  "traditional software" discipline re-enters the system.
- **Retrieval** — grounds the Model in facts outside its training data,
  directly addressing NIST's "data may be stale or detached from
  context" risk.
- **Memory** — persists state and context across time, since the Model
  itself has none.
- **Security** — the access-control and safety boundary around a
  component that can't fully self-police its own outputs.
- **Application** — the human-facing surface; translates the
  confederation's behavior into something a user can act on.
- **Diagnostics/Observability** — direct answer to NIST's "increased
  opacity" risk: visibility into a system that's harder to test than
  normal code.
- **Deployment Context Notes** — the same Model behaving differently
  under different operating constraints (API-service/Edge/RAG).

This is the same 9-node list `Standards/glossary.md`'s `AI` entry
already named at a one-line, per-node "what gap it covers" level (see
its "Applied to `rosetta-stone-AI`'s structure" section). This topic is
the next layer down: real Responsibility/Collaborator content per node,
not just the gap each one covers.

## Method

Per `Topics/collaborative-momentum-mode.md`'s operating principle — fast,
good-enough-not-perfect, grounded rather than recalled:

- Ground each node's Responsibilities/Collaborators in `rdd.pdf` (the
  RDD source text, see the `RDD` glossary entry) plus verified
  authoritative technical sources where a specific factual claim needs
  one (per `Standards/source-of-truth.md`'s basis rule), labeling
  anything that's Claude's own synthesis as `claude-reasoning` rather
  than presenting it as settled.
- No fixed order required across the 9 nodes — work through them in
  whatever order produces real content fastest.
- Also assess, while doing this, whether the 9-node list itself is
  complete — Bill's request explicitly includes "assess if any other
  nodes" belong. Don't just fill in the given list; check it.
- Write the result here (this topic file), not directly into XMind — see
  `Topics/xmind-copilot-collaboration.md`'s "whether to touch XMind at
  all" threshold rule for when/whether a map update is worth doing once
  this content exists.

## Status

Not started. Scope captured 2026-07-16 (Checkpoint 0016) so the next
session can begin directly rather than re-deriving the assignment.
Next session: Bill and Claude work through Responsibilities/Collaborators
per node, then start Q&A on the result once there's real content to
question — matching the same iterative process established for the `AI`
and `RDD` glossary entries.
