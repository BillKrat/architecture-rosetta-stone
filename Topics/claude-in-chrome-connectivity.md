---
name: claude-in-chrome-connectivity
description: Recurring Claude-in-Chrome domain-lockout bug when connecting to XMind Cloud, and the confirmed per-session workaround.
status: open — workaround confirmed, no permanent upstream fix
last-updated: 2026-07-13
---

## The bug

Claude-in-Chrome (`claude-in-chrome` MCP) runs under
`chromePermissionMode: "follow_a_plan"`. Under that mode, whichever
domain is approved by the *first-ever* `navigate()` call in a session
gets written into that session's `chromeAllowedDomains` and frozen
there for the session's entire lifetime — every later attempt to
navigate to a different domain (e.g. `app.xmind.com`) is silently
hard-denied (`Navigation to this domain is not allowed`), with no
prompt ever offered to approve the new domain. Nothing short-lived
fixes this: not reinstalling the extension, not changing
`claude.ai/settings/browser-extension`, not restarting Chrome.

This is a known upstream bug:
[anthropics/claude-code#74366](https://github.com/anthropics/claude-code/issues/74366)
(root-caused via that issue's comment thread). **It recurs on every new
Claude Code session** — the allowlist is per-session, not per-account
or per-install — and will keep recurring until Anthropic ships a fix.

## Refinement found 2026-07-12

The original 2026-07-11 writeup assumed the fix was "navigate to the
real target domain first, not a throwaway test domain." That's
necessary but not sufficient: on 2026-07-12, the first navigation of a
fresh session went straight to `https://www.xmind.works` (a real
Xmind-related domain, not a test one) — but that domain turned out to
be dead (browser error page on every load). The freeze happened anyway,
regardless of whether the domain actually resolved, leaving the session
locked out of `app.xmind.com` just the same as a throwaway-test-domain
mistake would have.

**Corrected rule: the first navigation of the session must go straight
to a domain you've confirmed actually loads.** For this project, that
domain is `https://app.xmind.com` — not `www.xmind.works`.

## Standing procedure

1. **At the start of any new session that will use Claude-in-Chrome for
   XMind**, make the very first `navigate()` call go directly to
   `https://app.xmind.com`. Do not "test" connectivity with
   `example.com` or any other placeholder first — that throwaway domain
   would itself get permanently frozen in.
2. **If already locked out** (discovered via a
   `Navigation to this domain is not allowed` error): the fix requires
   editing that session's local state file while the Claude desktop app
   is fully closed.
   - Fully quit Claude (Cmd+Q, not just closing the window).
   - Run the session-specific fix script generated for that session
     under `Artifacts/XMind/` (see below) — it patches
     `chromeAllowedDomains` in
     `~/Library/Application Support/Claude/claude-code-sessions/<workspace>/<dir>/local_<session-id>.json`
     to add `app.xmind.com`.
   - Reopen Claude, resume the same session, retry.
   - **A new fix script must be generated each time** — the session id
     (and therefore the state-file path) changes every session, so a
     prior session's script won't target the current one.
3. This is purely a client-side/session workaround; it does not change
   any account-level or extension-level setting, so it must be redone
   for every future session until upstream ships a fix.

## Incident record

- [Artifacts/XMind/2026-07-11_claude-in-chrome-permission-issue.md](../Artifacts/XMind/2026-07-11_claude-in-chrome-permission-issue.md) + paired fix script (renamed `.command` -> `.command.md` 2026-07-13 so Bill could send it to a work colleague evaluating Claude + the Chrome extension — some transfer channels balk at `.command` attachments; content unchanged) — first occurrence, root-cause writeup.
- [Artifacts/XMind/2026-07-12_claude-in-chrome-permission-issue.md](../Artifacts/XMind/2026-07-12_claude-in-chrome-permission-issue.md) + paired `.command` — recurrence, refined the "must actually resolve" rule.

## Open question

No permanent fix exists upstream as of 2026-07-12. Treat step 1 above
(navigate to `app.xmind.com` first, every session, every time) as
mandatory standing practice, not a one-time fix, until
[anthropics/claude-code#74366](https://github.com/anthropics/claude-code/issues/74366)
is resolved.
