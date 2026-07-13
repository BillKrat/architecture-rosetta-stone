---
name: glossary
description: Cross-project terminology, abbreviations, and their source of truth — starting with WDNA (Windows DNA).
status: established 2026-07-12; one entry (WDNA), now with a supporting MCSD/MSF comparison note
last-updated: 2026-07-13
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

**Related but distinct: MCSD / MSF (2026-07-13 finding)**

```yaml
basis: primary-source
quoted: >
  "MSF provides a set of models, principles, and guidelines for
  designing and developing enterprise solutions..." / "the process of
  describing the solution in terms of its organization, structure, and
  the interaction of its parts... breaks the problem into modules, and
  for each module identifies objects, services, attributes, and
  relationships" — Microsoft Official Curriculum 2710 (2710PRO.CHM,
  Bill's own MCSD-track study material, read directly by Claude
  2026-07-13).
```

Bill studied toward this material (course 2710, "Analyzing Requirements
and Defining Microsoft .NET Solution Architectures," the MCSD exam
70-300 prep book) years ago, before it went obsolete with Agile's rise
— initially misremembered as MCSE. Reviewed directly to check whether it
overlaps with or should inform WDNA. Finding: **it's a different,
unrelated Microsoft framework, not an alternate name or version of
WDNA.** It bundles two things, neither of which changes anything
established above:

- **MSF (Microsoft Solutions Framework)** — a *project process model*
  (Envisioning/Planning/Developing/Stabilizing/Deploying phases, waterfall
  vs. spiral tradeoffs). Governs project lifecycle, not architecture
  layers. Not adopted — superseded by Agile, same reason Bill's
  certification went obsolete.
- **Conceptual/Logical/Physical Design** (a step within MSF's Planning
  phase) — a *responsibility-discovery method* ("identify objects,
  services, attributes, relationships" from use cases), the same
  lineage as Wirfs-Brock's Responsibility-Driven Design that
  `rosetta-stone-AI` already uses, just less rigorous. Not adopted as a
  replacement for RDD; RDD is already the more disciplined version of
  the same idea. The three-way *label* (Conceptual/Logical/Physical) may
  be useful later purely as a way to talk about which project phase a
  piece of content belongs to (e.g. Phase 4/5 gap-analysis and
  requirements work) — not decided, not needed now.

Net effect: WDNA (tier placement) and RDD (responsibility definition
within a tier) remain exactly as already established. This entry exists
so the comparison doesn't have to be re-run if the question comes up
again.
