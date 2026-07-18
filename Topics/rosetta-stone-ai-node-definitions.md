---
name: rosetta-stone-ai-node-definitions
description: Responsibilities and Collaborators for rosetta-stone-AI's 9 core nodes (Model, Agent, Tool, Retrieval, Memory, Security, Application, Diagnostics/Observability, Deployment Context Notes), grounded in RDD Chapters 4-5 and the existing CRC card draft, plus an assessment of possibly-missing nodes.
status: Q&A in progress 2026-07-17 — Model node underway; Responsibilities and Agent-as-collaborator understood, Retrieval-as-collaborator flagged ambiguous (deferred to Retrieval's own Q&A), task/responsibility ownership still open; Agent/Tool/Retrieval/Memory/Security/Application/Diagnostics/Deployment Context Notes not yet started
last-updated: 2026-07-17
---

## Method and grounding

Per `Topics/collaborative-momentum-mode.md`'s explicit "immediate next
step," this is **not** a from-zero definition exercise. The starting
draft is `Artifacts/XMind/mcp-ai-components-crc-card-analysis.txt` (the
7-node CRC map Bill produced in ~5 minutes, 2026-07-14), confirmed
against `rosetta-stone-AI`'s existing content and refined against RDD's
actual formal treatment of Responsibilities and Collaborations.

**New grounding this session, closing a gap Checkpoint 0015 flagged
explicitly:** `rdd.pdf` Chapters 4 ("Responsibilities," p.109) and 5
("Collaborations," p.150) — previously unscanned — were read directly
this session. Core definitions now confirmed from the source rather than
inferred from Chapter 1 alone:

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
  one-line tag, per the RDD glossary entry's own note that this was "a
  candidate lightweight addition... the next time nodes are touched."
  RDD's own caution applies here too: "Don't worry about giving an
  object the 'right' stereotype... intended to help get you started
  thinking about your candidates, not to bog you down" (p.93) — treat
  these tags as a first pass, not a final classification.

Basis for what follows: `claude-reasoning`, built on the `authoritative`
RDD source above plus the existing CRC card artifact (itself an
unguarded, previously-produced draft, not independently authoritative)
and the already-established `AI` glossary entry's NIST-grounded
"gap each node covers" framing. Not exhaustive — meant to be questioned,
per the operating principle in `Topics/collaborative-momentum-mode.md`.

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

### Q&A log, 2026-07-17 (raw findings, not yet folded into the bullets above)

Bill's explicit call: hold edits to the Responsibility bullets above
until enough of the Q&A has happened to state them clearly for "the next
ignorant developer," rather than revise mid-stream. This log preserves
what the Q&A actually established, so the eventual rewrite is grounded
in it rather than reconstructed from memory later. Model's own Q&A isn't
finished — task/responsibility ownership is still open, deferred by
Bill to a future session.

- **"Linguistic/structured input" is not vectors.** It names the *form*
  of what arrives (natural language text, or structured formats like
  JSON/code/schemas) — both arrive as plain text, not vectors. Vectors
  (embeddings) are what that text becomes *after* parsing, one step
  later — the first bullet compressed "what comes in" and "what it
  becomes" into one clause, which is what caused the confusion. Needs
  a reword that separates those two explicitly.
- **Concrete walkthrough that exposed Model's real (narrow) boundary:**
  uploading a document and querying it (RAG, Lewis et al. 2020) does
  **not** send the document to the Model at any point. Chunking, text
  extraction, embedding the chunks, storing the vectors, embedding the
  query, and running the similarity search are all done by Retrieval/
  Memory/pre-processing — Model never touches the file and doesn't know
  it exists. Model's only real involvement is generating a response from
  whatever text got assembled into its context window by Agent (see the
  new Agent bullet above). This directly connects to Bill's own DCI
  reading (`adventuresontheedge.net`, the Direct Corpus Interaction
  paper) — DCI's critique is specifically of this chunk-then-top-k
  pattern, proposing an Agent that searches/reads the corpus directly
  via Tool calls instead of being fed pre-chunked fragments.
- **The similarity-search step vs. Model's "apply learned reasoning"
  step are categorically different, not just sequential.** The search
  step compares two vectors against a precomputed, stored index — fixed
  math, no learned reasoning happening in that moment. Model's
  generation step runs the current context through already-trained
  weights to synthesize new text. Neither one touches training data
  directly: **the Model has no access to training data at inference
  time at all** — training data shaped the weights once, during
  training, and is not present or consultable afterward. This corrects
  a very natural but wrong mental model ("the model looks things up in
  what it was trained on") that's worth stating explicitly for whoever
  reads this next, per Bill's own framing of the goal.
- **Bill's own synthesis, worth preserving close to verbatim:** a
  smaller context window means less material for Agent to assemble and
  hand to the Model — important information isn't so much "forgotten"
  as it is *crowded out/replaced* by newer material competing for the
  same limited space. Correctly derived from the corrected model above,
  not something I need to add to — flagging it here so it survives into
  whatever the polished version says about context-window constraints.
- **Worked pseudocode, 2026-07-17 (new — see `Topics/pseudocode-driven-comprehension.md`
  for the process this came from):** Bill wrote and iterated a
  `prepareForUpload`/`Chunk`/`dalVectorStore`/`sendYourQuery` example to
  test his own grasp of the upload/query flow. The core insight it
  surfaced: **a vector is only useful if whatever finds it can also
  retrieve what it was a vector of** — his first draft returned the
  whole original document text alongside the chunk vectors, losing the
  index-for-index pairing between each vector and its own source chunk.
  Fixed by carrying `Chunk(Text, Embedding)` pairs together through
  storage rather than letting the vectors and their text travel
  separately. This is the same finding as the bullet above ("Model's
  only real involvement...") restated at implementation-detail level —
  useful because it's where the abstract claim "Model never touches the
  document" turns into a concrete reason why upload-time code has to be
  written a specific way.

### Where Model's Collaborators understanding stands, 2026-07-17

Per Bill directly: Responsibilities are adequately understood. Of the
two Collaborators, **Agent** is understood well enough to move on (its
own dedicated Q&A is queued next). **Retrieval still reads as "broadly
ambiguous"** as a Model collaborator — Bill's own words, flagged
explicitly rather than glossed over, expected to resolve once Retrieval
gets its own Q&A pass rather than forced now. Task/responsibility
ownership (the specific question deferred at the end of Checkpoint
0018) is **still open** — this session's pseudocode work clarified the
Model/Retrieval boundary but didn't reach that specific question.

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
- **(action, added 2026-07-17 — Q&A finding)** Assemble the context
  window handed to the Model on each call: pull conversation/task state
  from Memory, pull relevant material from Retrieval, add system
  instructions and the current input, and combine them into the single
  prompt the Model actually sees. This was a real gap, not a restated
  existing bullet — surfaced when Bill asked who owns "Window Context"
  during Model Q&A and neither Model nor Memory turned out to be the
  right answer. Memory only supplies raw material on request (it's an
  information holder); deciding what to include, how much, and in what
  order is a decision, which belongs here.

### Collaborators
- **Model** — calls the Model to generate the next reasoning step or
  decision.
- **Tool** — invokes Tools for work the Model can't do reliably itself.
- **Memory** — consults conversation/task history to stay consistent
  across steps and avoid repeating failed approaches.
- **Application** *(added this pass — see "Corrections" below)* — is
  itself invoked by, and returns results to, the Application layer.

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
- **Memory** *(direction corrected this pass — see "Corrections" below)*

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
- **Retrieval** *(added this pass — see "Corrections" below)*

---

## Security

**Stereotype:** Controller — Security doesn't do the Application's or
Tool's work, it decides whether that work is allowed to happen.

### Responsibilities
- **(decision)** Filter/sanitize input and output — block injection
  attempts, redact sensitive output.
- **(decision)** Enforce identity and access control — confirm the
  requester (human or component) is allowed to do what it's asking.
- **(decision)** *(candidate addition, flagged not adopted — see
  "Open question 2" below)* Gate irreversible or high-impact actions
  behind explicit approval, distinct from access control itself.

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
  loads from *(added this pass — see "Corrections" below)*.

---

## Diagnostics/Observability

*(Not in the original 7-node CRC card — new this pass, grounded
directly in the `AI` glossary entry's NIST citation rather than drawn
from an existing draft.)*

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

*(Also new this pass. This one is structurally different from the other
8 — it isn't a component with its own runtime behavior, it's a set of
constraints that changes how **Model** behaves depending on where/how
it's deployed. Flagging that difference rather than forcing it into the
same shape as the others.)*

**Stereotype:** Does not cleanly fit RDD's six stereotypes — it's closer
to what RDD would call context/constraint documentation attached to the
Model's card than an independent collaborating object. Worth raising to
Bill directly (see "Open question 1" below) rather than silently
picking a stereotype that doesn't really apply.

### What this actually captures
- **(knowledge)** Documents that the *same* Model can behave differently
  under different operating constraints — API-service (hosted, elastic,
  network-dependent), Edge (local, resource-constrained, offline-capable),
  RAG-augmented (grounded by a specific Retrieval configuration) — per
  the `AI` glossary entry's note that this is "the same Model behaving
  differently under different operating constraints," not a different
  component.
- Not a Collaborator relationship in RDD's sense (no requests flow to or
  from "Deployment Context Notes") — it's metadata about the Model node,
  which is itself worth flagging as a modeling question (see below).

---

## Corrections found while grounding this pass

Cross-checking the CRC card's Collaborators lists against each other
(not just against RDD's guidance) surfaced two real asymmetries — a
node names another as a collaborator, but the reverse isn't recorded
anywhere:

1. **Memory → Application** was listed (Memory "interfaces with the
   Application to save and load user-specific states"), but
   **Application's** original Collaborators list didn't name Memory
   back. RDD's own collaboration diagrams (Figure 5-1) do show
   one-directional arrows as normal, so asymmetry isn't automatically a
   defect — but this specific case reads as an omission, not an
   intentional direction, since Application is described elsewhere as
   the actual persistence boundary Memory writes through. **Corrected
   above**: added Memory as an Application collaborator.
2. **Retrieval → Memory** was listed ("can store frequently retrieved
   items or utilize past search history"), but **Memory's** original
   list didn't name Retrieval back, for the same reason. **Corrected
   above**: added Retrieval as a Memory collaborator.
3. Also added **Agent → Application** explicitly on the Agent side —
   Application already listed Agent as a collaborator ("delegates... to
   the Agent"), but Agent's original list didn't name Application back,
   even though Agent's whole reason for existing is to serve requests
   that originate from Application and return results to it.

None of these are large findings, but they're exactly the kind of thing
RDD's own method is supposed to catch by walking the collaboration
network as a whole rather than trusting each card in isolation — and
exactly the kind of self-consistency check this project's prior
checkpoints (`RSK_RSAI_0001`-`0005`) already valued.

## Open questions for Bill

**1. Does "Deployment Context Notes" belong as a 10th sibling node, or
as metadata attached to Model's own card?** As written, it doesn't
participate in Responsibilities/Collaborators the way the other 8 do —
it's a note about how Model's behavior varies by deployment, not a
component with its own actions/knowledge/decisions. Two honest options:
keep it as-is (a deliberately different kind of entry, clearly marked as
such), or fold its content into Model's own card as a "Deployment
Variants" subsection and retire it as a standalone node. No strong
recommendation either way yet — flagging the structural oddity rather
than resolving it unilaterally.

**2. Does Security's "gate irreversible actions behind approval" belong
under Security, or as its own node?** The `vs-mcp-bridge` blog post
this session described an "approval-aware" boundary as architecturally
distinct from access control: Security decides *who's allowed to ask*;
approval decides *whether this specific action should actually happen*,
often with a human in the loop. Real system (`vs-mcp-bridge`'s proposal-
approval workflow) treats these as related but separably-testable
concerns. Listed above as a flagged candidate addition to Security, not
adopted as a new node — needs a decision, not a guess.

## Assessment: is the 9-node list complete?

Per Bill's explicit request to check this, not just fill in the given
list. Three candidates surfaced, deliberately kept to a short list
rather than expanding scope broadly:

- **Evaluation/Feedback** — a responsibility for judging whether output
  was actually *good* (quality scoring, human feedback capture,
  LLM-as-judge), distinct from Diagnostics/Observability (which records
  *what happened*, not whether it was right). Real gap: nothing in the
  current 9 nodes owns this. Candidate, not adopted.
- **Approval / human-in-the-loop gate** — see Open question 2 above;
  candidate either as Security's expanded scope or a distinct node.
- **Cost/Resource Management** — token budgeting, rate limiting,
  model/provider routing by cost — practically real for a paid-API
  product like `vs-mcp-bridge`, and not covered by any of the 9.
  Candidate, not adopted.

Deliberately **not** raising a "Training/Fine-tuning Pipeline" node —
that's a different lifecycle concern (how the Model's weights get
produced) than this map's scope (how a deployed AI system is
architected at runtime); out of scope rather than a gap, unless Bill
says otherwise.

## Status

First pass complete, 2026-07-17. Not pushed into `rosetta-stone-AI`'s
XMind map yet — per `Topics/collaborative-momentum-mode.md`'s "markdown
is source of truth" rule and the "juice worth the squeeze" threshold in
`Topics/xmind-copilot-collaboration.md`, this content should sit here
first; a map update is a separate, later decision once Bill has reviewed
it. Next: Bill's Q&A on this content, the two open questions above, and
the three candidate-node assessment.
