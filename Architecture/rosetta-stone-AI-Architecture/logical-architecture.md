---
name: logical-architecture
description: Data models, process diagrams, and system component models for the rosetta-stone-AI system.
status: mixed — System Component Models has real content (1 entry, contributed by Bill); Data Models and Process Diagrams still placeholder
last-updated: 2026-07-13
---

# Logical Architecture

The "how the pieces fit together" layer, still implementation-agnostic —
shape and flow, not technology choices (those belong in
[Physical & Technical Specs](physical-and-technical-specs.md)).

## Data Models

**What this collects:** The shape of the data each node reads, writes, or
owns — e.g. Memory's session/long-term state schema, Model's
input/output contracts, Retrieval's document/embedding shape. Logical
structure only; no database engine or storage technology decisions here.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## Process Diagrams

**What this collects:** The sequence/flow of how a request actually
moves through the nodes (e.g. Application -> Agent -> Tool/Retrieval/
Model -> back to Application) for representative scenarios — the runtime
choreography that `rosetta-stone-AI`'s Collaborator relationships imply
but don't themselves visualize. See the collaborator-relationship
diagram already produced this session (Claude Artifact, not yet
committed to this repo — see Checkpoint 0006's open follow-up) as a
starting reference for which nodes talk to which.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## System Component Models

**What this collects:** The mapping from `rosetta-stone-AI`'s
Responsibility nodes to actual deployable components/services, including
where one node maps to one service versus many-to-one or one-to-many.
This is where the Model (API-service)/(Edge)/(RAG) deployment variants
already documented in `rosetta-stone-AI` turn into real component
boundaries.

**Status:** 1 real entry below; otherwise not started.

**Owner:** (unassigned)

**Linked artifacts:** `SCM_RSAI_0001` below.

### SCM_RSAI_0001 — Credential Indirection and Secure Secret Management Service, placed in WDNA's Business Services tier

```yaml
id: SCM_RSAI_0001
type: SCM
scope: RSAI
status: active
basis: primary-source
quoted: >
  "Within the Windows DNA model, the Credential Indirection and Secure
  Secret Management Service belongs in the Business Services tier,
  specifically within the Security Services category." — Bill,
  contributed-windows-dna-credential-vault-context.md, section 2.
relationships:
  partOf: []
  dependsOn: [SEC_RSAI_0001]
```

A new component, not yet mapped to any existing `rosetta-stone-AI` node
(it's additive architecture-layer content, not a re-derivation of the
frozen vocabulary — see `../../Topics/bduf-freeze-and-training.md`).
Placed using `../../Standards/glossary.md`'s WDNA three-tier model as the
terminology source of truth, per Bill's contributed document
(`contributed-windows-dna-credential-vault-context.md`):

- **Tier:** Business Services (specifically its Security Services
  category) — not Presentation, not Data.
- **Boundary:** MCP processes run in the Business Services tier but
  never handle raw credentials directly. The Credential Vault Service
  mediates all credential usage; MCP-visible identifiers are opaque,
  non-derivable Credential Reference Identifiers (CRIDs) that map to
  encrypted credentials the Vault manages exclusively.
- **Adjacent Data Services tier component:** the encrypted credential
  store itself (e.g. SQLite or similar) — the store's *existence* is a
  Data Services concern, but the logic, policy, and access control
  governing it stay in Business Services. This is a Data Model
  candidate once that section has real content.
- **Security responsibilities** (encryption, KMS, access control, audit
  logging) are tracked separately as `SEC_RSAI_0001` in
  `system-policies.md` — this entry is about *where the component sits*
  in the tier model, not what it does internally.

**Status:** Active — conceptual, per the source document's own framing
("not a finalized standard or protocol specification... will evolve as
requirements mature"). Evolution path stated in the source: requirements
gathering -> detailed requirements -> component-level design ->
interface definitions -> security/operational hardening -> optional
RFC-style formalization.

**Owner:** (unassigned)
