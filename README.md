intelligence-agent — README.md + .gitignore PATCH — v1.3.0
===========================================================
Three changes. Apply in order.
===========================================================

CHANGE 1 — Suite table replacement
Find the existing suite table in README.md. It will contain rows referencing:
  SportMind/mcp-server
  SportMind/agent-examples
  SportMind/calibration-registry
(These repos do not exist)

Replace the entire suite table with:

| Repository | Role |
| --- | --- |
| SportMind/SportMind | Core library — the intelligence primitive set |
| SportMind/telegram-ai-bot-starter-kit | Telegram AI Bot Starter Kit |
| SportMind/fan-token-agentic-wallet-starter-kit | Fan Token Agentic Wallet Starter Kit |
| SportMind/intelligence-agent | This repository — monitoring, classification, briefing |

-----------------------------------------------------------

CHANGE 2 — Footer version
Find (exact):
  SportMind/intelligence-agent v1.0.0

Replace with:
  SportMind/intelligence-agent v1.2.0

Location: Footer of README.md.

-----------------------------------------------------------

CHANGE 3 — .DS_Store removal and .gitignore update

Step A: Add to .gitignore (if not already present):
  .DS_Store

Step B: Remove the committed .DS_Store file from the repo:
  git rm --cached .DS_Store
  (Then commit with the README changes)

Note: If .DS_Store is not in the repo root, check all subdirectories
and remove any committed instances.

===========================================================
All other README content unchanged.
===========================================================
