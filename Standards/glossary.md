---
name: glossary
description: Cross-project terminology, abbreviations, and their source of truth — starting with WDNA (Windows DNA).
status: established 2026-07-12; one entry so far
last-updated: 2026-07-12
---

# Glossary

Cross-project, like every other file in `Standards/` — a term defined
here applies everywhere, not just `rosetta-stone-AI`. Each entry
declares its `basis` per `Standards/source-of-truth.md`, same as any
other artifact — a glossary is not exempt from the rule just because
it's definitional rather than a requirement or risk.

## WDNA (Windows DNA)

```yaml
term: WDNA
fullName: Windows DNA (Windows Distributed interNet Applications Architecture)
basis: authoritative
citation:
  - https://news.microsoft.com/source/1997/09/23/microsoft-announces-comprehensive-architecture-for-next-generation-of-applications/
  - https://en.wikipedia.org/wiki/Windows_DNA
```

Microsoft's 1997 reference architecture for distributed, Internet-aware
enterprise applications — not a product, a strategy/road map (per
Microsoft's own framing) for building applications across three
logically separated tiers:

1. **Presentation Services** — the user interface and client-side
   interaction surfaces (in Microsoft's original technologies: browser,
   HTML, DHTML, client-side scripting; conceptually: any client
   application or interaction surface).
2. **Business Services** — business logic, workflow, rules engines, and
   cross-cutting enterprise services (security, identity, transaction
   management) that mediate between presentation and data.
3. **Data Services** — databases, storage engines, and persistent data
   management.

Superseded by the Microsoft .NET Framework as an active product
strategy, but the three-tier *pattern* it named is still a legitimate,
citable reference architecture — which is exactly the role Bill wants it
to play here (source of terminology, not something to literally
reimplement in COM/ActiveX).

**Abbreviation note:** `WDNA` is **not** an abbreviation Microsoft itself
used — their own materials say "DNA" or "Windows DNA" in full. Bare
`DNA` collides badly with the biological term and would be genuinely
ambiguous in this project's prose, so `WDNA` is **this project's own
disambiguating convention** (Bill's proposal, adopted 2026-07-12), not
an external standard. Flagging that distinction explicitly, per
`Standards/source-of-truth.md`: the three-tier *model* is
`authoritative`; the *abbreviation* `WDNA` is not — it's ours.

**Role in this project:** Bill's framing (2026-07-12): "WDNA as the
source of truth for our terminology" — i.e., when this project needs a
name for an architectural layer or a term for how components are
organized across tiers, WDNA's vocabulary (Presentation/Business/Data
Services) is the canonical reference to check against, rather than
inventing new terms ad hoc. First real application: placing the
Credential Indirection and Secure Secret Management Service (see
`Architecture/rosetta-stone-AI-Architecture/logical-architecture.md`,
`SCM_RSAI_0001`) within the Business Services tier.

**Not yet done:** a full mapping of `rosetta-stone-AI`'s own nodes
(Application, Agent, Tool, Retrieval, Memory, Security, Model) onto
WDNA's three tiers. Bill referenced wanting to see "that map" again to
refresh his memory before going further with this — treat that as the
next step in this thread, not something to pre-empt here.
