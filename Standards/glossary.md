---
name: glossary
description: Cross-project terminology, abbreviations, and their source of truth — WDNA (Windows DNA) and MSF (Microsoft Solutions Framework), and the determination between them.
status: established 2026-07-12; 2 entries (WDNA, MSF)
last-updated: 2026-07-13
---

# Glossary

Cross-project, like every other file in `Standards/` — a term defined
here applies everywhere, not just `rosetta-stone-AI`. Each entry
declares its `basis` per `Standards/source-of-truth.md`, same as any
other artifact — a glossary is not exempt from the rule just because
it's definitional rather than a requirement or risk. One `##` entry per
term, per `Standards/document-layout.md`.

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
`authoritative`; the *abbreviation* `WDNA` is not — it's ours, coined on
purpose.

That coining round-tripped in a useful way, worth recording: on first
seeing `WDNA` used, Bill's own cursory-review instinct read it as *not*
a real Microsoft acronym and therefore invalid, and started substituting
bare `DNA` — the opposite of the intent. A closer look caught that the
project was deliberately coining it to avoid the biological-DNA
collision, not citing it as Microsoft's own term. Both readings are
findable from this entry as written; the note above exists specifically
so a fast skim doesn't repeat that misread.

**Role in this project:** Bill's framing (2026-07-12): "WDNA as the
source of truth for our terminology" — i.e., when this project needs a
name for an architectural layer or a term for how components are
organized across tiers, WDNA's vocabulary (Presentation/Business/Data
Services) is the canonical reference to check against, rather than
inventing new terms ad hoc. First real application: placing the
Credential Indirection and Secure Secret Management Service (see
`Architecture/rosetta-stone-AI-Architecture/logical-architecture.md`,
`SCM_RSAI_0001`) within the Business Services tier.

**Framework determination (2026-07-13):** checked against MSF/MCSD (see
the `MSF` entry below) — WDNA remains this project's standard for
architectural *layering*. Nothing about that determination is a hedge
or a "for now"; it's the answer to "WDNA or MCSD, or best of both,"
worked through below.

**Reference map, built 2026-07-13:** `rosetta-stone-WDNA-Reference`
(https://app.xmind.com/7oUcRnoy) — a standalone XMind map of WDNA's
three tiers with example children and one note, built as the deferred
task from `Sessions/2026-07-13_Checkpoint_0009_*.txt`. This map is a
generic WDNA teaching/reference tool (also doubled as a live demo for
Bill's work team — see the checkpoint for that context); it is **not**
the mapping described below.

**Still not done:** a full mapping of `rosetta-stone-AI`'s own nodes
(Application, Agent, Tool, Retrieval, Memory, Security, Model) onto
WDNA's three tiers. The reference map above is a prerequisite/warm-up
for this, not a substitute — treat this as the next step in this
thread.

## MSF (Microsoft Solutions Framework)

```yaml
term: MSF
fullName: Microsoft Solutions Framework
basis: primary-source
quoted: >
  "MSF provides a set of models, principles, and guidelines for
  designing and developing enterprise solutions..." / "the process of
  describing the solution in terms of its organization, structure, and
  the interaction of its parts... breaks the problem into modules, and
  for each module identifies objects, services, attributes, and
  relationships" — Microsoft Official Curriculum 2710, "Analyzing
  Requirements and Defining Microsoft .NET Solution Architectures"
  (2710PRO.CHM, the MCSD exam 70-300 prep material), read directly by
  Claude 2026-07-13 in the coding-session thread at Bill's request.
```

**Why this got checked at all:** Bill studied toward MCSD (Microsoft
Certified Solution Developer) certification for a couple of years,
before it went obsolete with Agile's rise, just before the final exam —
initially recalled as MCSE (Microsoft Certified Systems Engineer, a
different track), corrected after checking a 2003 backup server that
confirmed it was actually MCSD. Over 20 years removed from the material,
Bill asked whether it overlapped with or should inform WDNA before this
project committed further to WDNA as the standard. Reviewed directly
(coding session, 2026-07-13) rather than answered from memory, per
`Standards/source-of-truth.md`.

**Finding:** MSF is a different, unrelated Microsoft framework — not an
alternate name or earlier version of WDNA. It bundles two things:

- **The MSF process model** (Envisioning/Planning/Developing/
  Stabilizing/Deploying phases; waterfall vs. spiral tradeoffs) — a
  *project lifecycle* model, not an architecture-layering one. **Not
  adopted** — superseded by Agile, the same shift that obsoleted Bill's
  certification track in the first place.
- **Conceptual/Logical/Physical Design** (a step inside MSF's Planning
  phase) — a *responsibility-discovery method*: identify objects,
  services, attributes, and relationships from use cases. Same lineage
  as Wirfs-Brock's Responsibility-Driven Design, which
  `rosetta-stone-AI` already uses — just less rigorous. **Not adopted**
  as a replacement for RDD; RDD is the more disciplined descendant of
  the same idea, already the standard here. The three-way *label*
  (Conceptual/Logical/Physical) may be worth reusing later purely to
  talk about which project phase a piece of content belongs to (e.g.
  Phase 4/5 gap-analysis work) — not decided, not needed now.

**Framework determination (2026-07-13), answering Bill's direct
question — WDNA, MCSD, or best of both:** effectively already best of
both, but not as a literal blend of the two frameworks. **WDNA** stays
the standard for architectural *layering* (Presentation/Business/Data
Services — see the `WDNA` entry above). **RDD**, already embedded
throughout `rosetta-stone-AI`, stays the standard for *responsibility
definition within a layer* — it's the more rigorous version of what
MSF's Conceptual/Logical/Physical step was already gesturing at, so
nothing from MCSD's method needed importing. **MSF's project-process
model is explicitly rejected** — the same reason Bill's certification
went obsolete applies here too. Net effect: WDNA and RDD remain exactly
as already established; nothing here changes either.

**Status:** Settled, pending Bill's confirmation reading this restated
form (he confirmed the underlying finding when it was first written; not
yet confirmed this specific reorganization into its own entry).
