---
name: system-policies
description: Security, identity, and access control models for the rosetta-stone-AI system.
status: mixed — Security Model has real content (1 entry, contributed by Bill); Identity Model and Access Control Model still placeholder
last-updated: 2026-07-13
---

# System Policies

The "who's allowed to do what, and how do we know who's asking" layer —
turning `rosetta-stone-AI`'s Security node (and the pieces of
data-handling policy scattered across Memory and Tool) into enforceable
rules.

## Security Model

**What this collects:** The concrete implementation of the Security
node's Responsibilities from `rosetta-stone-AI` — authentication
mechanisms, threat model, and enforcement points. This is also the right
place to resolve the PII/data-handling ambiguity flagged by this
session's ownership audit (Security, Memory, and Tool each independently
claim a piece of data-handling policy with no stated precedence) —
resolving that split is in scope for this document, not a side project.

**Status:** 1 real entry below; the PII/data-handling precedence question
this section describes is still open (see `RSK_RSAI_0004` in
`risks-and-open-issues.md`) — the new entry below is a distinct,
additional component, not a resolution of that finding.

**Owner:** (unassigned)

**Linked artifacts:** `SEC_RSAI_0001` below.

### SEC_RSAI_0001 — Credential Vault Service: encryption, key management, access control, audit

```yaml
id: SEC_RSAI_0001
type: SEC
scope: RSAI
status: active
basis: primary-source
quoted: >
  "Store all authentication credentials in encrypted form within the
  data tier. Manage encryption keys externally via a secure Key
  Management System (KMS) or equivalent. Provide a centralized
  Credential Vault Service that: Decrypts credentials internally.
  Performs downstream authentication on behalf of MCP components.
  Returns only authentication results, roles, claims, or short-lived
  tokens. Enforces access control policies for each CRID. Logs all
  access for auditing and compliance." — Bill,
  ../contributed-windows-dna-credential-vault-context.md, section 4.2.
relationships:
  partOf: [SCM_RSAI_0001]
```

The security responsibilities of the Credential Vault Service placed in
`SCM_RSAI_0001` (`logical-architecture.md`) — this entry is what it
*does*, not where it sits. Core mechanism: credential indirection.
Nothing that talks to the vault (including MCP processes) ever sees a
raw credential — only an opaque, non-derivable Credential Reference
Identifier (CRID). The Vault:

- Stores credentials encrypted, in the Data Services tier.
- Manages encryption keys externally (KMS or equivalent) — keys are not
  co-located with what they encrypt.
- Decrypts internally and performs downstream authentication *on behalf
  of* the caller — callers get back results (auth success/failure,
  roles, claims, short-lived tokens), never the credential itself.
- Enforces access-control policy per CRID and logs every access for
  audit/compliance.

Stated benefits (source document, section 4.4): eliminates credential
exposure in MCP workflows, centralizes security-policy enforcement,
allows credential rotation without touching MCP components, and
provides auditability.

**Status:** Active — conceptual, same caveat as `SCM_RSAI_0001`: not a
finalized spec, will evolve.

**Owner:** (unassigned)

## Identity Model

**What this collects:** How users, services, and agents are identified
and authenticated across the system — who/what has an identity, how it's
issued, and how it's verified at each boundary.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

## Access Control Model

**What this collects:** Concrete authorization rules — who/what can do
what to which resource. Should explicitly state the precedence between
Security (sets policy), Memory (enforces consent/retention for stored
state), and Tool (declares PII handling for tool-call payloads) once
that's resolved, rather than leaving three independent claims standing.

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.
