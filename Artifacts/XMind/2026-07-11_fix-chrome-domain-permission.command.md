#!/bin/bash
# Fixes the Claude-in-Chrome domain-permission lockout described in
# 2026-07-11_claude-in-chrome-permission-issue.md, for this specific session
# (cliSessionId 145556ed-f9d7-4473-adfa-9fe1268d56ae, "Coding session").
#
# Adds app.xmind.com to that session's frozen chromeAllowedDomains list.
#
# Usage: Quit the Claude desktop app FULLY (Cmd+Q) first, then double-click
# this file in Finder (or run it) to apply the fix. Reopen Claude and resume
# the "Coding session" session afterward.

set -euo pipefail

SESSION_FILE="/Users/billkratochvil/Library/Application Support/Claude/claude-code-sessions/f0e02dda-0b33-4522-973a-300e5c0f7f2c/ad25cfaa-9030-40d7-8573-cda9334bf0e9/local_2f22cbcb-6f7c-4c1b-b879-257ed8c43723.json"
DOMAIN_TO_ADD="app.xmind.com"

echo "Claude-in-Chrome domain permission fix"
echo "======================================="
echo ""

if [ ! -f "$SESSION_FILE" ]; then
  echo "ERROR: session file not found at:"
  echo "  $SESSION_FILE"
  echo "The session may have been archived or its ID changed."
  echo ""
  read -p "Press Return to close..."
  exit 1
fi

if pgrep -x "Claude" >/dev/null 2>&1; then
  echo "ERROR: the Claude desktop app still appears to be running."
  echo "Quit it fully first (Claude menu > Quit, or Cmd+Q), then run this again."
  echo ""
  read -p "Press Return to close..."
  exit 1
fi

cp "$SESSION_FILE" "$SESSION_FILE.bak"
echo "Backed up session file to:"
echo "  $SESSION_FILE.bak"
echo ""

python3 - "$SESSION_FILE" "$DOMAIN_TO_ADD" <<'PYEOF'
import json, sys

path, domain = sys.argv[1], sys.argv[2]

with open(path) as f:
    data = json.load(f)

domains = data.get("chromeAllowedDomains", [])
if domain not in domains:
    domains.append(domain)
data["chromeAllowedDomains"] = domains

with open(path, "w") as f:
    json.dump(data, f)

print("chromeAllowedDomains is now:", domains)
PYEOF

echo ""
echo "Done. Reopen the Claude desktop app and resume the session titled"
echo "'Coding session', then retry navigating to app.xmind.com."
echo ""
read -p "Press Return to close..."
