---
name: system-policies
description: Security, identity, and access control models for the rosetta-stone-AI system.
status: scaffolded — placeholders only, no real content yet
last-updated: 2026-07-12
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

**Status:** Not started.

**Owner:** (unassigned)

**Linked artifacts:** none yet.

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
