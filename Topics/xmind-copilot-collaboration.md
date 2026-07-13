---
name: xmind-copilot-collaboration
description: How to reliably use XMind's built-in Copilot (driven via Claude-in-Chrome) for bulk edits to the mindmap, and the batch-scoping method that makes it reliable.
status: established method, with two known unreliable surfaces (chat-panel click targeting, AI landing-page Enter-submit) — see below
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

**Confirmed 2026-07-12 (second occurrence): this is not unique to the
in-document chat panel.** XMind's separate "Create with AI" landing page
(Home -> Create New -> Create with AI, a full-page "What would you like
to create today?" prompt box used to generate a brand-new map from
scratch) has the same bare-Enter-submits behavior. There, the failure
mode is worse than truncation: a multi-line prompt fired off multiple
partial submissions, each spawning a **separate new blank document**
("untitled", generic "Central Topic / Main Topic 1-4" placeholder
content) — seven of them from one attempt, burning roughly 21 XMind AI
credits for zero usable output. Treat "Enter submits, compose as a
single line" as a platform-wide rule for any XMind AI text-entry
surface, not just the in-document chat panel, until a surface is
individually confirmed to behave otherwise. After any XMind AI
generation request, check All Maps/Recents for unexpected extra
documents before trusting that a single clean result (or a clean
failure) occurred.

## Incident: unreliable click-targeting into the chat panel (2026-07-12)

Clicking into the in-document Copilot chat input by pixel coordinate,
based on a screenshot taken moments earlier, is not reliable — a layout
reflow between the screenshot and the click (e.g. from the panel's
content scrolling as prior chat history renders) can land the click on
the canvas behind the panel instead of the input field. When that
happens, subsequently "typing into the chat box" actually types onto
the canvas: a first incident merged typed text into a stray new topic
under an existing node; a follow-up attempt to clear the (wrongly
targeted) input with Cmd+A / Delete appeared to select and briefly
blank the entire canvas. Both were fully recoverable with Cmd+Z (5
undos total across the incident), but **don't assume a click "into the
chat box" landed there** — after any click intended for that panel,
take a fresh screenshot and confirm a text cursor is visible in the
input (or that typed text appears in the compose box) before proceeding
to type or submit. If in doubt, use `read_page` to get an accessibility
ref for the actual input element rather than reusing coordinates from
an earlier screenshot.

## Recovery verification: diff against the frozen repo copy

If an accidental edit to the live document is suspected (see incident
above), the fastest trustworthy way to confirm full recovery is a
structural diff against the frozen snapshot already committed to this
repo (`Artifacts/XMind/rosetta-stone-AI.xmind`), not screenshots or the
app's own visual state (a scroll-position blank screen can look
identical to real data loss). Method: have the live document downloaded
as a fresh `.xmind` file, then treat both the download and the repo copy
as zip archives —

```bash
unzip -oq path/to/downloaded.xmind -d downloaded/
unzip -oq Artifacts/XMind/rosetta-stone-AI.xmind -d repo/
```

— and diff `content.json` from each. A raw text diff of topic titles
alone is a fast first check; for full confidence, recursively compare
title + notes + markers + child structure per topic (ignoring volatile
fields like ids/timestamps) via a small Python script rather than
trusting `diff` on the raw JSON (key ordering can differ harmlessly).
Used 2026-07-12 to confirm a 5-undo recovery was byte-for-byte
identical to the frozen copy (141/141 topics matched across every
sheet) after the click-targeting incident above.

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
