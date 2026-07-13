---
name: risks-and-open-issues
description: Known governance issues in the rosetta-stone-AI vocabulary — currently the ownership-audit findings from 2026-07-12, each tracked as a Risk/Known Issue (RSK) that violates one of the requirements in requirements-and-use-cases.md.
status: active — 5 open findings, none resolved
last-updated: 2026-07-12
---

# Risks & Open Issues

Cross-cutting — a risk or known issue can concern any node or any other
category in this Architecture document, so it doesn't belong to one of
the 5 MSDN categories the way the other files do (see
`../../Standards/identifier-scheme.md` for why `RSK` got its own file).

**Important:** nothing here has been fixed in `rosetta-stone-AI` itself.
That document is frozen (`../../Topics/bduf-freeze-and-training.md`) —
these findings are recorded so Phase 1 training (and any future session)
has them on hand when it reaches the relevant nodes, not acted on ahead
of that process. Resolving a finding means either correcting
`rosetta-stone-AI` once it's unfrozen, or a conscious decision that the
current design is actually fine and the finding gets closed as
not-a-defect — either way, that's a decision for the training/
investigation process, not something pre-empted here.

All 5 below trace to the same source: a collaborator-relationship
diagram and ownership audit run against the frozen `rosetta-stone-AI`
map on 2026-07-12 (see `Sessions/2026-07-12_Checkpoint_0006_*.txt` for
how that work was done).

## RSK_RSAI_0001 — Diagnostics/Observability has no Owner

```yaml
id: RSK_RSAI_0001
type: RSK
scope: RSAI
status: open
relationships:
  violates: [RD_RSAI_0001]
```

The Diagnostics/Observability node in `rosetta-stone-AI` has full
Responsibilities, Metrics & Thresholds, and Acceptance Criteria fields,
but no `Owner:` field at all — the one node in the entire map with zero
owners, not one. It's also named as a collaborator, under three
different names, by other nodes: Tool lists "Monitoring", Model
(API-service) lists "Monitoring/Observability", Model (Edge) lists
"Central monitoring (aggregated telemetry)". Every other node also
carries its own Runbook/Dashboard block (e.g. `dashboard=DB-APP-01`),
so it's unclear whether Diagnostics/Observability is meant to own
cross-cutting telemetry infrastructure while each node owns its own
dashboard content, or whether it should own all of it and simply never
got assigned a name.

**Relevant node(s):** Diagnostics/Observability (primary); Tool, Model
(API-service), Model (Edge) (reference it inconsistently).

**Status:** Open.

## RSK_RSAI_0002 — Deployment-context responsibilities modeled twice, two owners

```yaml
id: RSK_RSAI_0002
type: RSK
scope: RSAI
status: open
relationships:
  violates: [RD_RSAI_0002]
```

The API-service/Edge/RAG deployment variants are defined in two places
with two different owners: as sub-topics under Model (`Model
(API-service)`, `Model (Edge)`, `Model (RAG)`), each with its own full
Owner/Responsibilities/Acceptance-Criteria block (owners: "API/model
infra owner", "Edge/model release owner", "RAG pipeline owner"); and
again in the separate "Deployment Context Notes" node, which defines
"API-service Responsibilities", "Edge Responsibilities", and "RAG
Responsibilities" under a single "Deployment owner (infra/devops)". If a
production incident hits the API-service deployment, the map currently
names two different accountable owners.

**Relevant node(s):** Model (API-service), Model (Edge), Model (RAG),
Deployment Context Notes.

**Status:** Open.

## RSK_RSAI_0003 — Provenance/grounding claimed by three owners

```yaml
id: RSK_RSAI_0003
type: RSK
scope: RSAI
status: open
relationships:
  violates: [RD_RSAI_0002]
```

Three different nodes, under three different owners, each hold a piece
of "make sure claims are sourced": Retrieval ("provide provenance" as a
core Responsibility; "provenance links" as a Runtime Hook), Model (RAG)
("attach provenance for each claim"; "provenance links in response"),
and Deployment Context Notes -> RAG ("ensure provenance is attached and
retrieval quality is monitored"). If a factual claim ships without
provenance, the map doesn't say which of the three (Retrieval/index
owner, RAG pipeline owner, Deployment owner) is accountable.

**Relevant node(s):** Retrieval, Model (RAG), Deployment Context Notes.

**Status:** Open.

## RSK_RSAI_0004 — PII / data-handling policy split three ways

```yaml
id: RSK_RSAI_0004
type: RSK
scope: RSAI
status: open
relationships:
  violates: [RD_RSAI_0002]
```

Security ("enforce data and usage policies"), Memory ("enforce access
controls, consent, TTL, and selective forgetting"; Regulatory Notes:
"GDPR/CCPA considerations, user data export/delete, consent records"),
and Tool (Regulatory Notes: "Data residency, PII handling, contractual
constraints") each independently claim a piece of PII/data-handling
policy. Plausible as an intentional division of labor (Security sets
policy, Memory enforces consent/retention for stored state, Tool
declares PII handling for tool-call payloads) — but the map never states
that hierarchy explicitly, so as written it reads as three independent
claims rather than one delegated chain.

**Relevant node(s):** Security, Memory, Tool.

**Status:** Open.

## RSK_RSAI_0005 — Takedown/DMCA handling worded near-identically in two places

```yaml
id: RSK_RSAI_0005
type: RSK
scope: RSAI
status: open
relationships:
  violates: [RD_RSAI_0002]
```

Retrieval's Regulatory Notes ("Source attribution, takedown/DMCA
handling, sensitive-data filters") and Model (RAG)'s Regulatory Notes
("Source attribution requirements, takedown handling, sensitive-source
filtering") describe what reads as the same underlying duty, written
into both nodes independently rather than assigned once and referenced.
Related to `RSK_RSAI_0003` (both involve Retrieval and Model (RAG)
overlapping on provenance-adjacent concerns) but distinct enough to
track separately — this one is specifically about legal/takedown
process, not grounding quality.

**Relevant node(s):** Retrieval, Model (RAG).

**Status:** Open.
