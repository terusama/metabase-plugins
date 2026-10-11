# Connect Velostics Metabase

Ask Claude Code or Codex questions about the Metabase data your organization has authorized you to access. You need an existing Velostics account with analytics access. No API key, local server, or velOS installation is required.

Preview: this package connects to staging data and requires an invited staging account. It is not a production analytics service.

## Install

Add the public marketplace, then install the plugin:

| Client | Add the marketplace | Install the plugin |
| --- | --- | --- |
| Claude Code | `claude plugin marketplace add terusama/metabase-plugins` | `claude plugin install velostics-metabase@velostics-metabase` |
| Codex | `codex plugin marketplace add https://github.com/terusama/metabase-plugins.git` | `codex plugin add velostics-metabase@velostics-metabase` |

Alternatively, download and extract the marketplace ZIP from the repository's releases. Open a terminal in its extracted folder and replace the marketplace address above with `.`.

Start a new conversation after installation. Ask: **"Help me connect Velostics Metabase."** The bundled setup skill explains how to sign in.

## Sign in and ask a question

1. In Claude Code, open `/mcp` and select the plugin's Metabase connection. In Codex, run `codex mcp login metabase` in your terminal.
2. Follow the sign-in action to open your browser. Use your existing Velostics account on the Velostics sign-in page.
3. Complete the browser flow and return to your conversation.
4. Ask: **"Show me the analytics I can access."**

After connecting, try **"Show me five recent records"** or **"Summarize the available shipment data."** The agent discovers the tables and fields available to your account before querying. If you see an access error, ask your organization's administrator to enable analytics for your account.

Sign-in happens in your browser. Never paste a password, access token, or Metabase API key into the conversation. The plugin requests analytics read access and does not provide SQL execution or data editing.

## Recover a connection

If the connection asks you to sign in again, repeat the sign-in step above. If your browser reports a callback mismatch, share that error with Velostics support; the publisher must register the client's callback URL. If the gateway is unavailable, retry the connection after a minute. Reinstalling the plugin does not grant additional data access.

To remove the plugin, run `claude plugin uninstall velostics-metabase@velostics-metabase` or `codex plugin remove velostics-metabase@velostics-metabase` in your terminal.

## Data handling

Your client sends analytics questions to the hosted gateway. The gateway verifies your identity and organization access before querying Metabase. Query results enter your agent conversation, where your Claude or Codex provider's data policies also apply. This archive contains public connection settings and instructions; it contains no user credentials or tenant data.

## Compatibility and release status

Browser sign-in, authorized queries, and denial of another tenant's table were verified in staging with Claude Code 2.1.296 and Codex 0.162.1 on October 11, 2026. Claude Desktop and public directory approval are separate distribution paths.
