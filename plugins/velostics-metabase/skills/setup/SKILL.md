---
name: setup
description: Help a user connect Velostics Metabase, sign in with their existing account, or recover an analytics connection.
---

Help the user connect the Metabase server supplied by this plugin.

1. Explain: "Sign in with your existing Velostics account to access your organization's analytics."
2. If the connection needs authentication, direct Claude Code users to `/mcp`, the plugin's Metabase connection, and its sign-in action. Direct Codex users to run `codex mcp login metabase` in their terminal. Let the client handle browser OAuth. Never request or collect passwords, tokens, or API keys in chat.
3. Once tools are available, use `search` to discover authorized analytics. Read the live tool schema before supplying arguments.
4. Report the names of the available tables or metrics. Invite a question about one of those sources.

For an access denial, explain that the account needs analytics permission from its organization administrator. Do not change accounts or tenant identifiers to bypass a denial. For callback errors, report the browser's error to the user and direct them to the publisher for configuration repair. For service errors, give a short retry instruction; do not claim a successful connection until a tool call succeeds.

Use the package's README for installation instructions. The connection settings in `connection.json` identify whether this is a preview or production deployment. Preview accounts access staging data.
