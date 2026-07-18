---
name: rosetta-stone-ai-node-definitions
description: Pristine reference — Stereotype, Responsibilities, and Collaborators for rosetta-stone-AI's 9 core nodes, grounded in RDD Chapters 4-5. Kept clean to study from; see rosetta-stone-ai-node-definitions-qa-log.md for correction history, open questions, and Q&A discovery notes.
status: Q&A in progress 2026-07-17 — Model's Responsibilities and Agent-as-collaborator understood, Retrieval-as-collaborator flagged ambiguous, task/responsibility ownership still open (see companion log); Agent/Tool/Retrieval/Memory/Security/Application/Diagnostics/Deployment Context Notes not yet started
last-updated: 2026-07-17
---

## Method and grounding

Per `Topics/collaborative-momentum-mode.md`'s explicit "immediate next
step," this is **not** a from-zero definition exercise. The starting
draft is `Artifacts/XMind/mcp-ai-components-crc-card-analysis.txt` (the
7-node CRC map Bill produced in ~5 minutes, 2026-07-14), confirmed
against `rosetta-stone-AI`'s existing content and refined against RDD's
actual formal treatment of Responsibilities and Collaborations.

**Grounding closes a gap Checkpoint 0015 flagged explicitly:** `rdd.pdf`
Chapters 4 ("Responsibilities," p.109) and 5 ("Collaborations," p.150) —
previously unscanned — were read directly. Core definitions confirmed
from the source rather than inferred from Chapter 1 alone:

- **Responsibilities** (p.110, direct quote basis): "general statements
  about software objects. They include three major items: the actions
  an object performs, the knowledge an object maintains, [and] major
  decisions an object makes that affect others." Every Responsibility
  below is written to fit one of those three categories, not as a loose
  feature list.
- **Collaborations** (p.150, direct quote basis): "requests from one
  object to another. One object calls on, or collaborates with, another
  because it needs something. The two objects work in concert to fulfill
  larger responsibilities." RDD explicitly warns (p.152) not to clutter
  a card with obvious collaborations and not to list an object as its
  own collaborator — applied below by keeping each Collaborators list to
  real, non-obvious dependencies only.
- **Object Role Stereotypes** (p.93-94): service provider, controller,
  coordinator, structurer, information holder, interfacer (with
  user/external/intersystem sub-types). Applied per node below as a
  one-line tag. RDD's own caution applies: "Don't worry about giving an
  object the 'right' stereotype... intended to help get you started
  thinking about your candidates, not to bog you down" (p.93) — treat
  these tags as a first pass, not a final classification.

Basis for what follows: `claude-reasoning`, built on the `authoritative`
RDD source above plus the existing CRC card artifact and the
already-established `AI` glossary entry's NIST-grounded "gap each node
covers" framing. Not exhaustive — meant to be questioned.

**A note on how this document stays clean:** this file holds only
settled, current content — a Responsibility or Collaborator appears here
once it's actually part of the definition, not while it's still a
candidate or under discussion. Correction history, open questions,
candidates not yet adopted, and per-node Q&A discovery notes all live in
the companion file, `Topics/rosetta-stone-ai-node-definitions-qa-log.md`
— equally valuable, deliberately kept separate so this document reads
as a reference, not a running log.

---

## Model

**Stereotype:** Service provider (does the work of generating output on
request; not a controller — it doesn't decide what happens next in the
larger flow, that's Agent).

### Responsibilities
- **(action)** Parse linguistic/structured input into an internal
  representation suitable for generation.
- **(action)** Generate output — text, code, or structured data — from
  the context and instructions it's given.
- **(action)** Apply learned reasoning patterns (deductive/inductive) to
  problems posed in the prompt.
- **(knowledge)** Maintains no persistent knowledge of its own beyond
  training-time weights — this is the load-bearing fact from the `AI`
  glossary entry's NIST grounding: Model is "the only node whose
  behavior is genuinely learned/trained rather than coded."

### Collaborators
- **Agent** — provides the reasoning "engine" the Agent calls to decide
  what to do next; the Model doesn't initiate anything on its own.
- **Retrieval** — receives grounding context from Retrieval to reduce
  reliance on stale or absent training data (directly answers NIST's
  stale/detached-data risk, per the `AI` glossary entry).

---

## Agent

**Stereotype:** Controller/coordinator hybrid — decides what happens
next (controller-like) but does not perform the substantive work itself,
delegating it to Model/Tool (coordinator-like). RDD doesn't sharply
force these apart in the source text reviewed; flagging the hybrid
rather than picking one arbitrarily.

### Responsibilities
- **(decision)** Decompose a high-level goal into a sequence of smaller
  sub-tasks.
- **(decision)** Select which Tool or Model call happens next, based on
  current task state.
- **(action)** Manage the iteration loop (observe → decide → act) until
  the goal is met or a stopping condition is hit.
- **(action)** Assemble the context window handed to the Model on each
  call — pull conversation/task state from Memory, pull relevant
  material from Retrieval, add system instructions and the current
  input, and combine them into the single prompt the Model actually
  sees.

### Collaborators
- **Model** — calls the Model to generate the next reasoning step or
  decision.
- **Tool** — invokes Tools for work the Model can't do reliably itself.
- **Memory** — consults conversation/task history to stay consistent
  across steps and avoid repeating failed approaches.
- **Application** — Agent is invoked by, and returns results to, the
  Application layer that initiated the request.

---

## Tool

**Stereotype:** Service provider — the clearest case of the six.
Performs a well-defined unit of work on request and nothing more.

### Responsibilities
- **(action)** Execute a specific, narrowly-scoped, deterministic task
  (run code, query a database, fetch live data) that the Model cannot
  do reliably itself.
- **(action)** Normalize raw external results into a structured form the
  Agent/Model can consume.

### Collaborators
- **Agent** — receives parameters from, and returns results to, the
  Agent; Tool never initiates work on its own.
- **Security** — every Tool invocation passes through sandboxing/
  permission checks before it's allowed to run.

---

## Retrieval

**Stereotype:** Service provider, information-holder-adjacent (it
doesn't originate the knowledge, but it's responsible for finding and
ranking it).

### Responsibilities
- **(action)** Search external stores (vector indices, document
  collections) for content relevant to the current query.
- **(decision)** Rank and filter candidates so only the most relevant
  material reaches the context window — a real decision, not just a
  passthrough, since it determines what the Model sees.

### Collaborators
- **Model** — supplies grounding context the Model uses to reduce
  hallucination and reliance on stale training data.
- **Memory** — can store frequently-retrieved items or draw on past
  search history to refine future retrieval strategies.

---

## Memory

**Stereotype:** Information holder.

### Responsibilities
- **(knowledge)** Maintain the short-term buffer for the current
  session/conversation.
- **(knowledge)** Persist longer-term state (preferences, past outcomes)
  across sessions.

### Collaborators
- **Agent** — supplies the context an Agent needs to stay consistent
  across a multi-step task.
- **Application** — the Application is Memory's actual persistence
  boundary (load/save to a real store); Memory doesn't persist itself
  end-to-end.
- **Retrieval** — draws on Memory's stored history (frequently-retrieved
  items, past searches) to refine its own future retrieval strategy.

---

## Security

**Stereotype:** Controller — Security doesn't do the Application's or
Tool's work, it decides whether that work is allowed to happen.

### Responsibilities
- **(decision)** Filter/sanitize input and output — block injection
  attempts, redact sensitive output.
- **(decision)** Enforce identity and access control — confirm the
  requester (human or component) is allowed to do what it's asking.

### Collaborators
- **Application** — validates credentials at the system's entry point.
- **Tool** — enforces execution-time policy (sandboxing, path/network
  restrictions) around what a Tool is allowed to touch.

---

## Application

**Stereotype:** Interfacer (user interfacer specifically, per RDD's
sub-types) plus coordinator for session/state lifecycle.

### Responsibilities
- **(action)** Present the interface (web/mobile/CLI/IDE surface) a
  human uses to submit requests and see output.
- **(action)** Initialize and manage the lifecycle of a user session.
- **(decision)** Route requests to the Agent and decide how/when final
  results are delivered back to the user.

### Collaborators
- **Agent** — delegates goal execution to the Agent; is where the
  Agent's results ultimately surface.
- **Security** — requests authentication/authorization before
  processing any input.
- **Memory** — is the actual persistence boundary Memory saves to and
  loads from.

---

## Diagnostics/Observability

*(Not in the original 7-node CRC card — grounded directly in the `AI`
glossary entry's NIST citation rather than drawn from an existing
draft.)*

**Stereotype:** Information holder / service provider hybrid — it holds
a record of what happened and provides that record on request; it does
not act on the system itself.

### Responsibilities
- **(knowledge)** Maintain a durable, structured record of what actually
  happened — which tool ran, what input/output crossed each boundary,
  what approval or policy decision applied (directly modeled on the
  boundary logging already described in the `vs-mcp-bridge` "Understanding
  AI Chat Sessions, Models, and Agents" post: request ids, tool
  descriptors, policy decisions, correlation).
- **(action)** Surface that record in a form a human can review after
  the fact — this is the direct, concrete answer to NIST AI 100-1
  Appendix B's "increased opacity" risk (per the `AI` glossary entry):
  opacity isn't solved by trusting the Model more, it's solved by making
  its actual behavior inspectable independent of the Model's own
  self-report.

### Collaborators
- **Agent** — records the Agent's tool calls and decisions as they
  happen, not reconstructed after the fact from the Model's own account.
- **Security** — records what was allowed/denied and why, so an approval
  or policy decision is itself auditable.

---

## Deployment Context Notes

*(This entry is structurally different from the other 8 — it isn't a
component with its own runtime behavior, it's a set of constraints that
changes how **Model** behaves depending on where/how it's deployed. See
the companion log for the open question this raises about whether it
belongs as a standalone node at all.)*

**Stereotype:** Does not cleanly fit RDD's six stereotypes — it's closer
to what RDD would call context/constraint documentation attached to the
Model's card than an independent collaborating object.

### What this actually captures
- **(knowledge)** Documents that the *same* Model can behave differently
  under different operating constraints — API-service (hosted, elastic,
  network-dependent), Edge (local, resource-constrained, offline-capable),
  RAG-augmented (grounded by a specific Retrieval configuration) — per
  the `AI` glossary entry's note that this is "the same Model behaving
  differently under different operating constraints," not a different
  component.
- Not a Collaborator relationship in RDD's sense (no requests flow to or
  from "Deployment Context Notes") — it's metadata about the Model node.

---

## See also

For correction history, open questions, the missing-node assessment, and
per-node Q&A discovery notes, see
[`Topics/rosetta-stone-ai-node-definitions-qa-log.md`](rosetta-stone-ai-node-definitions-qa-log.md) —
kept separate so this document stays clean to study from.
