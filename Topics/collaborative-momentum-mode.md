---
name: collaborative-momentum-mode
description: The working mode that replaced BDUF gating on 2026-07-14 — no more freeze/phase-checkpoint gates blocking progress; Standards and existing artifacts kept as reference, not constraints; goal is momentum toward real vs-mcp-bridge development.
status: active — adopted 2026-07-14, supersedes the gating half of bduf-freeze-and-training
last-updated: 2026-07-14
---

## What changed, and why

Four calendar days (2026-07-12 through 2026-07-14) of BDUF process —
frozen maps, a 9-field-per-node training curriculum, checkbox-gated
phase sign-off, a "Coding Session is mentoring-only, no coding, no
updates" boundary — produced real infrastructure (Standards/, the
Architecture/ document set, two frozen maps, a working persistence
system) but **zero progress on the actual objective**: Bill
understanding AI/Model/Application/etc. well enough to co-develop
`vs-mcp-bridge`. The Application node's three opening questions
(Checkpoint 0005) were never answered — every session that opened with
"let's code" got diverted into something else (Standards authoring, a
demo, git archaeology, a map comparison) before reaching that actual
work.

The triggering comparison (2026-07-14): Bill had a separate, unguarded
5-minute prompt produce `Artifacts/XMind/mcp-ai-components-crc-card-analysis.txt`
— a 7-node CRC-card model (Application, Model, Agent, Tool, Retrieval,
Memory, Security — the same core seven `rosetta-stone-AI` has) that is
internally consistent, technically accurate, and immediately usable, with
no contradictions found on review. `rosetta-stone-AI`, by contrast, after
four days of heavy process, has real internal defects (see
`Architecture/rosetta-stone-AI-Architecture/risks-and-open-issues.md`'s
`RSK_RSAI_0001`-`0005`, plus independently-found gaps: empty Model
(API-service)/(Edge) leaves, Cross-cutting fields structurally
misrepresented as a tenth component) that the process itself never
caught — a human reading the content critically caught them, the same
way this comparison did, in minutes.

Bill's diagnosis, confirmed and adopted: **the heavy process didn't
produce correctness, and it consumed the time that should have gone to
the one thing that mattered.** Grounding in real, verifiable facts (per
`Standards/source-of-truth.md`) is what makes an answer trustworthy, not
the ceremony wrapped around it. Bill's own successful precedent — an
"impossible" 2.5-day deliverable that led to a company bid-defense win —
was fast *and* fact-grounded (POs, architects, source code), not fast
*because* it skipped rigor. That's the model going forward: speed and
truth-grounding together, not speed traded against rigor, and not rigor
used as a substitute for actually doing the work.

## What's removed

- The `rosetta-stone-AI` / `rosetta-stone-MCP-Bridge` content freeze
  ("no modification and no investigation" — `bduf-freeze-and-training.md`'s
  "working agreement" section). Both maps may now be read, discussed,
  and edited directly as part of real work.
- The checkbox-gated, 9-field-per-node Phase 1 training curriculum as a
  *precondition* for anything else happening. Comprehension now builds
  through direct, momentum-first work, not a prerequisite drill.
- The "Coding Session is mentoring-only, no coding, no updates, route
  ideas elsewhere" boundary (`bduf-freeze-and-training.md`, "Session
  scope, tightened 2026-07-13"). One session, one thread of real work.
- The strict phase sequencing (train -> re-investigate -> repeat on
  Concern B -> gap analysis -> requirements/backlog) as a required order.
  These may still happen, but not as a gate nothing else can proceed
  without.

## What's kept — explicitly, per Bill's own words

"I'm not suggesting we throw away anything that we've done in regards
to architectural standards and practices... there can be no constraints
that prevent us from moving forward." Kept as **reference and working
material**, not gates:

- WDNA (Windows DNA — Presentation/Business/Data Services) as the
  project's terminology for architectural layers.
- `Standards/` in full — identifier scheme, relationship vocabulary,
  source-of-truth basis rule, document-layout templates, glossary.
- The `Architecture/rosetta-stone-AI-Architecture/` document set and
  everything real already in it (Requirement Definitions, the 5 tracked
  Risks, the Credential Vault artifact).
- Both frozen maps' *content* as a starting draft/reference — not
  discarded, just no longer gated behind a freeze.
- The persistence discipline itself (git as source of truth,
  Sessions/Topics/INDEX) — this checkpoint is written using exactly that
  system.

## The new operating principle

Fast, momentum-first, good-enough-not-perfect definitions of AI/Model/
Application/etc. — just solid enough that Bill and Claude share a
working understanding and can start real collaborative development on
`vs-mcp-bridge`. Depth (metrics, failure modes, ownership, runbooks —
the fields `rosetta-stone-AI` has beyond Responsibilities/Collaborators)
gets added when real work actually needs it, not pre-specified upfront.
Bill's framing, verbatim: "the problem can't be solved by the same mind
that created it, if you are not going to be solution oriented, I'll have
to do it myself" — both people at the table are expected to bring real,
independent judgment, not agreement-seeking.

## Immediate next step

Use the CRC card map (`Artifacts/XMind/mcp-ai-components-crc-card-analysis.txt`)
as the working starting draft for what AI/Model/Application/Agent/Tool/
Retrieval/Memory/Security mean in this project, confirm it against
`rosetta-stone-AI`'s existing content where they overlap, and move
toward real `vs-mcp-bridge` code — not a new lengthy definition exercise
from zero.
