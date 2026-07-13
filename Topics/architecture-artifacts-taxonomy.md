---
name: architecture-artifacts-taxonomy
description: Superseded — the MSDN-style architecture-artifact taxonomy moved from a planned XMind map to markdown files under Architecture/rosetta-stone-AI-Architecture/. Kept for the incident history (why XMind was rejected for this job).
status: superseded — see Architecture/rosetta-stone-AI-Architecture/ for the live version
last-updated: 2026-07-12
---

## Why this exists

Bill wants to "overload the use of our XMind application" — use it for
more than the AI-vocabulary work in `rosetta-stone-AI`. This is a
separate, parallel initiative: a standing taxonomy of architecture
artifact types (requirements docs, data models, API contracts, security
models, DR plans, etc.) that future project work can hang concrete
deliverables off of. It is unrelated in content to `rosetta-stone-AI`
and `rosetta-stone-MCP-Bridge` — a new document, not a branch added to
either existing one.

## Naming decision

Proposed and used (not yet confirmed by Bill, but consistent with the
existing `rosetta-stone-<Topic>` naming convention of the other two
maps): **`rosetta-stone-Architecture-Artifacts`**.

## Required taxonomy (Bill's spec, verbatim structure)

Standard: Microsoft/MSDN application architecture guidance style.
Central topic: "Architecture Artifacts". Exactly 5 top-level branches,
each with the listed children (additional closely-related, commonly
paired artifact types may be added under a branch if it strengthens
completeness — but every listed item must be present):

1. **Requirements & Use Cases** -> Business Requirements Document,
   Functional Specifications, User Stories
2. **Logical Architecture** -> Data Models, Process Diagrams, System
   Component Models
3. **Physical & Technical Specs** -> Technology Choices, API Contracts,
   Infrastructure Topology Mappings
4. **System Policies** -> Security Model, Identity Model, Access
   Control Model
5. **Operational Plans** -> Disaster Recovery (DR) Plans, Monitoring
   Strategy, Rollout / Rollback Plan

Structure: 2 levels only (top-level category -> artifact type), no
deeper nesting required.

## First attempt (2026-07-12) — failed, cleaned up

Used XMind's "Create with AI" landing page (Home -> Create New -> Create
with AI) with the full spec above written as a prompt. The prompt was
typed with embedded newlines (a numbered list, matching the structure
above) — this hit the same bare-Enter-submits UI quirk already known for
the in-document Copilot chat (see
`Topics/xmind-copilot-collaboration.md`), except on this surface the
failure mode was worse: each embedded Enter fired a partial submission,
and the flow spawned **seven separate blank "untitled" documents**
(generic "Central Topic / Main Topic 1-4" placeholder, none of the
requested taxonomy content), consuming ~21 XMind AI credits for zero
usable output. All seven were manually moved to Trash (right-click ->
Move to Trash) and the workspace was confirmed clean (only the two real
maps remain).

**No `rosetta-stone-Architecture-Artifacts` document exists yet.**

## Next attempt — what to change

Compose the generation prompt as a **single line, no embedded
newlines** — use plain-language enumeration (e.g. "branch 1 is X with
children A, B, C; branch 2 is Y with children D, E, F; ...") instead of
a real numbered list with line breaks. After submitting, check
All Maps/Recents for unexpected extra "untitled" documents before
trusting the result, and verify the generated structure actually
contains all 5 branches and their required children (the AI may
still take liberties even with a clean single-line prompt) before
treating this as done.

## Superseded 2026-07-12

After the failed attempt above, Bill raised a real scalability concern:
a single flat XMind canvas, growing for the *lifetime* of the project,
risks becoming exactly the "densely populated, unnavigable" kind of map
he'd seen elsewhere. Discussed alternatives (GitHub wiki vs. an in-repo
markdown folder) and settled on the latter, to keep one unified git
history rather than fragmenting into a second `.wiki.git` repo.

The live version of this work is now
`Architecture/rosetta-stone-AI-Architecture/` — a folder of markdown
files (one per MSDN category, plus a `README.md` index), not an XMind
map. See `Architecture/rosetta-stone-AI-Architecture/README.md` for the
current structure and naming convention
(`rosetta-stone-<Concern>-Architecture`).

This file is kept, not deleted, because the XMind attempt and its
failure are real incident history worth preserving — the "Enter
submits" lesson recorded in `Topics/xmind-copilot-collaboration.md` came
directly from it.

## Open questions (as of the XMind attempt — now moot)

- ~~Confirm the proposed name (`rosetta-stone-Architecture-Artifacts`)~~
  — superseded; the live document uses `rosetta-stone-AI-Architecture`
  per the naming convention above.
- ~~Decide whether this new map should also get a frozen
  `Artifacts/XMind/` snapshot~~ — moot; it's markdown in this repo now,
  already git-native.
