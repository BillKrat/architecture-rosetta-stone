---
name: xmind-copilot-collaboration
description: How to reliably use XMind's built-in Copilot (driven via Claude-in-Chrome) for bulk edits to the mindmap, and the batch-scoping method that makes it reliable.
status: established, reusable method
last-updated: 2026-07-12
---

## Context

The `rosetta-stone-AI` XMind Cloud map had a pre-existing formatting
defect: roughly 122 topic titles across the map carried a stray leading
bullet-dot prefix (`• ` solid bullet or `◦ ` hollow bullet) baked into
the title text itself — not a list-style artifact, actual characters.
Before any real architecture-content work could start, these needed
stripping to give a clean canvas. That cleanup (2026-07-12) is also
where this method was worked out.

## What doesn't work

Asking XMind Copilot to fix "every topic in the entire map" in one
request. On the first attempt, Copilot:

- Tried a single ~104-operation batch edit.
- Got confused distinguishing the two different bullet glyphs in use
  (`•` vs `◦`) and whether a bullet shown in its own tool output was
  real title content or a rendering artifact.
- Mismatched exact titles against hidden leading-space/indentation
  noise in its own `get_sheet` output.
- Spiraled through several minutes of uncertain, self-contradicting
  reasoning ("maybe this was already correct," "maybe the edit was a
  no-op," etc.).
- Ultimately made almost no real edits, yet reported "Done." twice.

**Lesson: don't trust a Copilot "Done." at face value on a large or
ambiguous request.** Verify against its own diff log (it shows an
explicit `-`/`+` per changed topic when it actually edits something) or
by independently re-reading the outline — not the chat transcript's
prose summary.

## What works reliably

Scope each request to one branch/parent at a time (roughly 7-15 topics
per batch), and **hand Copilot the exact literal old-text titles to
match**, rather than asking it to figure out on its own which titles
need fixing. Every batch run this way succeeded cleanly in a single
pass, and at a small fraction of the credit cost of the failed
whole-map attempt (a 9-item scoped batch cost ~4 credits vs. ~39
credits burned by the confused whole-map attempt that mostly failed).

Concrete pattern used successfully:

```
In the "<Branch>" branch only, rename exactly these N topics by
deleting only their literal leading "◦ " (or "• ") prefix, leaving the
rest of each title byte-for-byte identical:
1. "<exact old title 1>"
2. "<exact old title 2>"
...
Do not touch any other topic in this pass.
```

## UI quirk: Enter submits, don't embed real newlines

The Copilot chat input submits on a bare `Enter` — it is not
Shift+Enter-for-newline like typical chat UIs. A prompt typed with
literal embedded newlines (e.g. a numbered list, one item per line)
gets **prematurely cut off mid-message**: only the text up to the first
newline actually sends, and the remainder is left sitting unsent in the
compose box (which can look like it sent, since the box scrolls and a
"Thinking" spinner may appear from the truncated fragment). Compose
multi-item batch prompts as a **single line** (no embedded newlines) —
use plain-language enumeration or slash/semicolon separators instead of
a real numbered list with line breaks.

## Verification method

After every batch:
- Read Copilot's own "Updated mindmap" diff block inline (exact `-`/`+`
  per topic) to confirm the edit actually happened, not just that it
  said "Done."
- Independently pull the live outline (`get_page_text` / `read_page` on
  the Outliner view) after a full page reload and grep for stray bullet
  glyphs, rather than trusting the chat's own summary of what changed.

## Result (2026-07-12 cleanup)

All ~122 bullet-prefixed topic titles cleaned across: Application,
Model, Model (RAG), Agent, Tool, Retrieval, Memory, Security,
Deployment Context Notes, and Cross-cutting fields branches. Verified
clean via full-map reload + outline text dump. No other content
(topic colors, tree structure, body/note text) was altered — confirmed
by diffing Copilot's own change log line-by-line against the intended
scope.

## Reusable takeaway

This method (small branch-scoped batches + exact literal target text +
diff-log verification, avoiding both whole-map requests and multi-line
prompts) is the standing approach for any future bulk-edit request to
XMind Copilot on this map, not just this one cleanup pass.
