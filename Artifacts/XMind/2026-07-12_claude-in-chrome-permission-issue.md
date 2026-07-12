# Claude in Chrome — Domain Permission Lockout, recurrence (2026-07-12)

## Summary

Same bug as [2026-07-11_claude-in-chrome-permission-issue.md](2026-07-11_claude-in-chrome-permission-issue.md)
(upstream [anthropics/claude-code#74366](https://github.com/anthropics/claude-code/issues/74366)),
recurring in a new session with a worse outcome: the domain that got frozen
into `chromeAllowedDomains` turned out to be dead.

## What happened

At the start of this session, following the "navigate to the real target
first, not a throwaway test domain" lesson from the 2026-07-11 doc, the first
`claude-in-chrome` navigation was directly to `https://www.xmind.works` (the
Xmind-related domain used in a prior working session).

That domain loaded to a browser error page (`Frame with ID 0 is showing error
page` on every subsequent screenshot/get_page_text call — confirmed dead
across a reload, not a transient load timing issue). Because
`chromePermissionMode` is `follow_a_plan`, that first navigation still
permanently froze `www.xmind.works` as the session's one allowed domain,
regardless of it being unusable.

Subsequent navigation to `https://app.xmind.com` (the real XMind app domain)
was hard-denied: `Navigation to this domain is not allowed`.

**Lesson refinement:** the fix isn't just "navigate to the real target
domain first" — it's "navigate to a domain you've *confirmed loads*." A
first navigation to a dead or wrong domain is just as costly as a throwaway
test domain, since `chromeAllowedDomains` freezes on the first attempt
regardless of whether it actually succeeded. `www.xmind.works` should not be
used again as a first-navigation target; go straight to `app.xmind.com`.

## This session's details

```
Session file: ~/Library/Application Support/Claude/claude-code-sessions/f0e02dda-0b33-4522-973a-300e5c0f7f2c/ad25cfaa-9030-40d7-8573-cda9334bf0e9/local_4fd647b4-cf05-443e-a06c-c4254791150a.json
sessionId:     local_4fd647b4-cf05-443e-a06c-c4254791150a
cliSessionId:  259a107f-b203-409e-b9f4-b240d931cb0b
title:         "Coding session"
chromePermissionMode: follow_a_plan
chromeAllowedDomains (frozen, before fix): ["www.xmind.works"]
chromeTabGroupId: 1927177768
```

## Workaround

Same procedure as 2026-07-11, applied to this session's file. A ready-to-run
script for this specific session is at
[2026-07-12_fix-chrome-domain-permission.command](2026-07-12_fix-chrome-domain-permission.command):

1. **Fully quit** the Claude desktop app (Claude menu → Quit, or Cmd+Q — not
   just closing the window).
2. Double-click `2026-07-12_fix-chrome-domain-permission.command` in Finder
   (or run it from a terminal). It backs up the session file, adds
   `app.xmind.com` to `chromeAllowedDomains`, and reports the result.
3. Reopen the Claude desktop app and resume the session titled **"Coding
   session"**.
4. Retry navigation to `app.xmind.com`.

## References

- [2026-07-11_claude-in-chrome-permission-issue.md](2026-07-11_claude-in-chrome-permission-issue.md) — original root-cause writeup
- [anthropics/claude-code#74366](https://github.com/anthropics/claude-code/issues/74366)
