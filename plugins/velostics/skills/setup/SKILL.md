---
name: setup
description: Connect Velostics, sign in with an existing Velostics account, or recover the website and analytics connection.
---

Connect Velostics using the Velostics connection supplied by this plugin.

1. Check whether the connection is already authenticated. If it is, proceed to discovery without asking the user to sign in again.
2. If authentication is needed, explain: "Sign in with your Velostics account in the browser, then return here. I'll show you what your account can access." Direct Claude Code users to `/mcp`, the plugin's Velostics connection, and its sign-in action. For Codex, run `codex mcp login velostics` when terminal execution is available, or give that one command to the user. Let the installed client handle browser OAuth. Never collect passwords, tokens, or API keys in chat.
3. Read live tool schemas. Use `velostics_api_search` for website operations or `search` for analytics sources, according to the user's request. Website access does not require an analytics membership.
4. Report the accessible resources from a successful call, then proceed with the user's task.

For an access denial, explain that the account needs the corresponding website or analytics permission from its organization administrator. An older token may need a new browser sign-in after a plugin upgrade to request website API access. Do not change accounts or tenant identifiers to bypass a denial. For callback errors, report the browser's error and direct the user to the publisher for configuration repair. For service errors, give a short retry instruction; do not claim a successful connection until a tool call succeeds.

Use the package's README for installation instructions. The connection settings in `connection.json` identify whether this is a preview or production deployment. Preview accounts access nonproduction data.
