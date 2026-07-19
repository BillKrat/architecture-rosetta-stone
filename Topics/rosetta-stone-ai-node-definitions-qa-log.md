---
name: rosetta-stone-ai-node-definitions-qa-log
description: Companion to rosetta-stone-ai-node-definitions.md — correction history, open questions, the missing-node assessment, and per-node Q&A discovery notes. Kept separate so the main reference document stays pristine to study from.
status: active, grows alongside node-by-node Q&A
last-updated: 2026-07-19
---

## Purpose

`Topics/rosetta-stone-ai-node-definitions.md` is meant to read as a
clean reference — Stereotype, Responsibilities, and Collaborators per
node, nothing else. This file holds everything about *how* that content
reached its current state: corrections found while grounding it,
questions still open, candidates considered but not adopted, and the
raw discovery notes from each node's Q&A session. Equally valuable —
deliberately kept out of the document Bill studies from directly, per
his explicit request (2026-07-17): "I'd like to keep the documents I am
learning from pristine."

## Corrections found while grounding the first pass (2026-07-17)

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
   the actual persistence boundary Memory writes through. **Corrected**:
   Memory added as an Application collaborator.
2. **Retrieval → Memory** was listed ("can store frequently retrieved
   items or utilize past search history"), but **Memory's** original
   list didn't name Retrieval back, for the same reason. **Corrected**:
   Retrieval added as a Memory collaborator.
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

## Wording correction found during Agent's Q&A (2026-07-19)

Bill caught, during Agent's dedicated Q&A, that both **Agent**'s Tool
collaborator line and **Tool**'s own Responsibilities bullet said the
Model "can't do **reliably**" the examples given (run code, query a
database, fetch live data). "Reliably" implies Model has some native
capacity there that just needs backup — not true for these specific
examples: Model has no execution environment, no live network/database
access, no mechanism to touch anything outside its own forward pass
over trained weights. It's a hard incapacity, not a reliability gap —
the same boundary the Model Q&A already established ("the Model has no
access to training data at inference time at all"). **Corrected**: both
lines now read "can't do itself" / "cannot do itself," dropping
"reliably."

Flagged for later, not acted on now: there *are* real reliability-only
cases (e.g. precise arithmetic on large numbers, exact date math) where
Model can attempt the work and sometimes gets it wrong rather than being
categorically unable — if a future Tool Responsibility is added that's
actually that kind of case, "reliably" would be the right word there,
just not for the three examples currently listed.

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
concerns. Candidate Responsibility, not adopted into Security's card yet:
"(decision) Gate irreversible or high-impact actions behind explicit
approval, distinct from access control itself." Needs a decision, not a
guess.

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

## Model — Q&A log (2026-07-17)

Bill's explicit call: hold edits to the pristine document's
Responsibility bullets until enough of the Q&A has happened to state
them clearly for "the next ignorant developer," rather than revise
mid-stream. This log preserves what the Q&A actually established, so the
eventual rewrite is grounded in it rather than reconstructed from memory
later. Model's own Q&A isn't finished — task/responsibility ownership is
still open, deferred by Bill to a future session.

- **"Linguistic/structured input" is not vectors.** It names the *form*
  of what arrives (natural language text, or structured formats like
  JSON/code/schemas) — both arrive as plain text, not vectors. Vectors
  (embeddings) are what that text becomes *after* parsing, one step
  later — the pristine doc's first Model bullet compresses "what comes
  in" and "what it becomes" into one clause, which is what caused the
  confusion. Needs a reword that separates those two explicitly, once
  Model's Q&A is far enough along.
- **Concrete walkthrough that exposed Model's real (narrow) boundary:**
  uploading a document and querying it (RAG, Lewis et al. 2020) does
  **not** send the document to the Model at any point. Chunking, text
  extraction, embedding the chunks, storing the vectors, embedding the
  query, and running the similarity search are all done by Retrieval/
  Memory/pre-processing — Model never touches the file and doesn't know
  it exists. Model's only real involvement is generating a response from
  whatever text got assembled into its context window by Agent (see
  Agent's context-assembly Responsibility in the pristine doc). This
  directly connects to Bill's own DCI reading (`adventuresontheedge.net`,
  the Direct Corpus Interaction paper) — DCI's critique is specifically
  of this chunk-then-top-k pattern, proposing an Agent that searches/
  reads the corpus directly via Tool calls instead of being fed
  pre-chunked fragments.
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
  reads this next.
- **Bill's own synthesis, worth preserving close to verbatim:** a
  smaller context window means less material for Agent to assemble and
  hand to the Model — important information isn't so much "forgotten"
  as it is *crowded out/replaced* by newer material competing for the
  same limited space.
- **Worked pseudocode, 2026-07-17** (see
  `Topics/pseudocode-driven-comprehension.md` for the process this came
  from): Bill wrote and iterated a
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

### Where Model's Collaborators understanding stands (2026-07-17)

Per Bill directly: Responsibilities are adequately understood. Of the
two Collaborators, **Agent** is understood well enough to move on (its
own dedicated Q&A is queued next). **Retrieval still reads as "broadly
ambiguous"** as a Model collaborator — Bill's own words, flagged
explicitly rather than glossed over, expected to resolve once Retrieval
gets its own Q&A pass rather than forced now. Task/responsibility
ownership (the specific question deferred at the end of Checkpoint
0018) is **still open** — the pseudocode work clarified the
Model/Retrieval boundary but didn't reach that specific question.

### Model Q&A closed (2026-07-19)

Per Bill directly: Model is checked off — no pseudocode warranted for
Retrieval at Model's altitude, a plain-language explanation was enough
(Retrieval finds/ranks grounding content; Agent, not Model, is the one
that actually calls Retrieval and assembles its results into the
context window Model sees — see the Agent-mediation point already
established above). Retrieval-as-a-Model-collaborator stays exactly as
flagged: a candidate, not settled.

**Bill's own hypothesis, worth preserving verbatim-adjacent:** as the
remaining nodes get their own Q&A passes, Retrieval may turn out to be
*only* a Collaborator of Agent, not of Model directly — leaving it
listed under Model's Collaborators, as-is, risks reading as more
settled than it is and could confuse a future reader. This is flagged
as Bill's candidate hypothesis (`claude-reasoning`-adjacent but
attributed to Bill, not verified against RDD independently), to be
tested when Retrieval gets its own dedicated Q&A rather than resolved
now by editing the pristine doc.

## Blog capture note

Per Bill (2026-07-17): the `vs-mcp-bridge` blog posts are a supplement
to this reference chain, not part of it. Once a post moves out of
repo-only-draft status into the backlog and is actually published,
reference links back to it can be added here (or in the pristine doc)
as applicable — not before. Two posts exist as unpublished drafts so
far: "What Is AI? A Grounded Definition" and "Understanding the Model
Node: What It Actually Does (and Doesn't Do)."
