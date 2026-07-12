# Claude in Chrome — Domain Permission Lockout (2026-07-11)

## Summary

During today's session, Claude (via the `claude-in-chrome` MCP browser tools) was unable to
navigate to or interact with `app.xmind.com` — the exact site needed to open
`rosetta-stone-AI.xmind`. Every attempt failed with either:

- `Navigation to this domain is not allowed` (from `navigate`)
- `Permission denied for this action on this domain` (from `computer`/screenshot/click)

This happened even though:
- The account-level setting at `claude.ai/settings/browser-extension` → "Default for all sites"
  was set to **"Allow extension."**
- The "Blocked sites" list was empty.
- The Chrome extension's own "approved sites" list (`chrome-extension://.../options.html`) was
  empty, with no user-facing way to manually add a domain to it.
- `example.com` worked fine in the same tab/session throughout.

It worked last night. It stopped working this morning, in a brand-new session.

## Root cause (confirmed via upstream bug report)

This is a known, reproduced bug — [anthropics/claude-code#74366](https://github.com/anthropics/claude-code/issues/74366).
Root-cause analysis by GitHub user `NAQasem` (comment
[here](https://github.com/anthropics/claude-code/issues/74366#issuecomment-4895074132)):

The Claude desktop app persists a **per-session** browser domain allowlist in that session's
local state file:

```
~/Library/Application Support/Claude/claude-code-sessions/<workspace-id>/<dir-id>/local_<session-id>.json
```

Relevant fields:

```json
"chromePermissionMode": "follow_a_plan",
"chromeAllowedDomains": ["<the one domain approved when the session first navigated anywhere>"]
```

Every `claude-in-chrome` MCP call passes this mode + list to the extension. In the extension's
`checkPermission` logic, when `chromePermissionMode` is `follow_a_plan` and
`chromeAllowedDomains` is non-empty, **any hostname not already in that list is hard-denied**
(`needsPrompt: false`) — meaning the normal "ask the user to approve this new site" prompt path
is never reached. No prompt ever appears anywhere (not in-page, not in the extension panel, not
in the desktop app) because the code path that would show it is unreachable once the list is
frozen.

**Nothing ever updates `chromeAllowedDomains` after the session's first navigation.** The
allowlist is captured once, at session start, and stays frozen for the life of that session —
regardless of extension reinstalls, Chrome restarts, or account-level settings changes.

## The specific cause in *this* session

We located and read this session's actual state file:

```
~/Library/Application Support/Claude/claude-code-sessions/f0e02dda-0b33-4522-973a-300e5c0f7f2c/ad25cfaa-9030-40d7-8573-cda9334bf0e9/local_4f190f28-f2a3-4514-b5f5-cd17388d0af1.json
```

```json
{
  "sessionId": "local_4f190f28-f2a3-4514-b5f5-cd17388d0af1",
  "cliSessionId": "3525059f-4771-49ee-acac-0fd0744047ee",
  "title": "Claude CLI default installation",
  "chromePermissionMode": "follow_a_plan",
  "chromeAllowedDomains": ["example.com"],
  "chromeTabGroupId": 1354507712
}
```

The `chromeTabGroupId` matches the exact browser tab group used throughout this conversation,
confirming this is the file in control.

**Why `example.com` and not `xmind.com` got frozen in:** early in this session, Claude's first
action was a connectivity *test* — navigating to `https://example.com` to confirm the Chrome
extension was working at all, before any Xmind-related request had been made. That test
navigation was the session's first-ever domain approval, so it became the permanent (and only)
entry in `chromeAllowedDomains` for this session's lifetime. Every subsequent attempt to reach
`app.xmind.com` (the domain actually needed) was hard-denied as a result — not because of any
misconfiguration, but because a diagnostic action taken before the real task began accidentally
consumed the session's one allowed slot.

**Lesson for future sessions:** don't "test" `claude-in-chrome` connectivity by navigating to an
arbitrary throwaway domain first. Under `follow_a_plan` mode, whichever domain is approved
*first* in a session becomes the *only* domain that session can ever reach. If a real target
domain is already known, navigate there first (or skip the test navigation entirely).

## Why it "worked last night" but not this morning — the disaster-preparedness clue

We also inspected a second, earlier session file from the same day:

```
~/Library/Application Support/Claude/claude-code-sessions/f0e02dda-0b33-4522-973a-300e5c0f7f2c/ad25cfaa-9030-40d7-8573-cda9334bf0e9/local_2f22cbcb-6f7c-4c1b-b879-257ed8c43723.json
```

```json
{
  "sessionId": "local_2f22cbcb-6f7c-4c1b-b879-257ed8c43723",
  "cliSessionId": "145556ed-f9d7-4473-adfa-9fe1268d56ae",
  "title": "Coding session",
  "chromePermissionMode": "follow_a_plan",
  "chromeAllowedDomains": ["www.xmind.works"],
  "chromeTabGroupId": 1725049026
}
```

This session's frozen allowlist is `www.xmind.works` — i.e., in that session, the first domain
ever navigated to was an Xmind-related domain, so Xmind access worked seamlessly for the rest of
that session's life. This matches the **`lets-code` / `update-context` disaster-preparedness
test** run yesterday: recovering session context from scratch and re-verifying the Xmind
checkpoint workflow would naturally have caused Xmind to be the very first domain touched,
which is exactly why "it worked last night" — the lucky ordering of that session, not a
difference in account configuration, explains the discrepancy between the two sessions.

## Workaround

Per the upstream issue's confirmed workaround, editing the frozen list requires the desktop app
to be fully closed (editing while it's running risks the app overwriting the edit with its
unchanged in-memory state):

1. **Fully quit** the Claude desktop app (Claude menu → Quit, or Cmd+Q — not just closing the
   window).
2. Open this session's state file in a text editor:
   ```
   open -e "/Users/billkratochvil/Library/Application Support/Claude/claude-code-sessions/f0e02dda-0b33-4522-973a-300e5c0f7f2c/ad25cfaa-9030-40d7-8573-cda9334bf0e9/local_4f190f28-f2a3-4514-b5f5-cd17388d0af1.json"
   ```
3. Change:
   ```json
   "chromeAllowedDomains":["example.com"]
   ```
   to:
   ```json
   "chromeAllowedDomains":["example.com","app.xmind.com","claude.ai"]
   ```
4. Save and close the file.
5. Reopen the Claude desktop app and resume the session titled **"Claude CLI default
   installation"**.
6. Retry navigation to `app.xmind.com` in that resumed session.

This is a **per-session** fix — it does not change any account-level or extension-level setting,
and a brand-new future session will start with an empty/single-domain allowlist again, subject to
whatever domain happens to be approved first in that new session.

### Verified working

After quitting the app, editing `chromeAllowedDomains` to
`["example.com","app.xmind.com","claude.ai"]`, and resuming the session, the state file confirmed
the edit had persisted (`chromeAllowedDomains` unchanged after resume, `lastActivityAt` updated).
On resume, a fresh browser tab group was created automatically (a new `chromeTabGroupId`, distinct
from the one recorded at the top of this doc) — this is expected; the domain allowlist travels
with the session regardless of which physical tab group is currently attached.

Navigation to `https://app.xmind.com/YCY6x8b0` then succeeded immediately, with no permission
error, and a follow-up screenshot successfully rendered the live `rosetta-stone-AI` mind map
(Charter node, Mission Statement branch, and the Charter / Investigation Protocol / Responsibility
Investigation Framework tabs) — confirming full read/interact access was restored.

## Upstream bug report filed

A bug report describing this session's symptoms was drafted for
[anthropics/claude-code](https://github.com/anthropics/claude-code/issues), consistent with the
existing open issue [#74366](https://github.com/anthropics/claude-code/issues/74366) (and related
[#74696](https://github.com/anthropics/claude-code/issues/74696)) that already documents the same
root cause and workaround.

## References

- [anthropics/claude-code#74366](https://github.com/anthropics/claude-code/issues/74366) — root
  cause and workaround, confirmed via GitHub API comment thread.
- [Claude in Chrome permissions guide](https://support.claude.com/en/articles/12902446-claude-in-chrome-permissions-guide)
- [Claude in Chrome troubleshooting](https://support.claude.com/en/articles/12902405-claude-in-chrome-troubleshooting)
