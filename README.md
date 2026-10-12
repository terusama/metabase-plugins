# Connect Velostics

Use your Velostics account in Claude Code or Codex to find records, query data, and make the changes you can make on the website.

Preview: this package connects to staging data and requires an invited staging account. Use it only with staging records.

## Connect and ask

1. Ask your assistant: **"Connect Velostics."** It will check the connection and guide you to sign in if needed.
2. Sign in with your Velostics account in the browser, then return to your conversation. An existing sign-in session can take you straight back.
3. Ask: **"Show my Velostics profile"**, **"Find my upcoming appointments"**, or **"Show five recent analytics records."** To make a change, describe what you want changed.

Sign-in happens on `login.velostics.com`; keep passwords out of the conversation. Your account needs website access for website operations and analytics access for Metabase queries. A permission denial means the account cannot perform that request.

## Install once

Add the public marketplace, then install the plugin:

| Client | Add the marketplace | Install the plugin |
| --- | --- | --- |
| Claude Code | `claude plugin marketplace add terusama/metabase-plugins` | `claude plugin install velostics-metabase@velostics-metabase` |
| Codex | `codex plugin marketplace add https://github.com/terusama/metabase-plugins.git` | `codex plugin add velostics-metabase@velostics-metabase` |

Alternatively, download and extract the marketplace ZIP from the repository's releases. Open a terminal in its extracted folder and replace the marketplace address above with `.`.

Start a new conversation after installation, then follow **Connect and ask** above. No API key, local server, or velOS installation is required.

## Open sign-in yourself

| Client | Start sign-in |
| --- | --- |
| Claude Code | Open `/mcp`, select this plugin's **Metabase** connection, and choose its sign-in action. |
| Codex | Run `codex mcp login metabase` in your terminal. |

The browser page names the client you should return to. The connection retains the name **Metabase** so existing installations keep working. Never paste a password, access token, or Metabase API key into the conversation.

The plugin requests website API access and analytics read access. The website still decides which records and changes your account can access. Analytics tools query Metabase and do not execute raw SQL or edit analytics data.

## Website operations

The assistant searches registered operations, inspects the selected operation, and sends a read or a change through your website permissions. It does not need a URL or a tenant credential from you.

| Tool | Use |
| --- | --- |
| `velostics_api_search` | Find operations by resource, action, or method. |
| `velostics_api_get_operation` | Inspect an operation's method, path parameters, and formats. |
| `velostics_api_read` | Read a registered operation. |
| `velostics_api_write` | Make the change you requested through a registered operation. |

Reads and changes use separate tools. Ask for the exact change you want; the assistant should clarify an ambiguous target or action before writing. A change can send notifications or start work just as it does on the website. Do not automatically retry a change after a timeout.

## Recover a connection

If asked to sign in again, use the sign-in action above. After upgrading, sign in again if website tools report a missing API permission. For an access error, ask your organization's administrator to check your account permissions. For a callback mismatch, share the error with Velostics support. If the service is unavailable, retry after a minute. Reinstalling does not grant additional record access.

To remove the plugin, run `claude plugin uninstall velostics-metabase@velostics-metabase` or `codex plugin remove velostics-metabase@velostics-metabase` in your terminal.

## Data handling

Your client sends requests to the hosted gateway, which verifies your sign-in. Website calls go to Velostics with your user identity; Metabase queries resolve your organization's analytics access. Results enter your agent conversation, where your Claude or Codex provider's data policies also apply. This archive contains public connection settings and instructions; it contains no user credentials or tenant data.

## Compatibility and release status

The previous analytics preview was verified in staging with Claude Code 2.1.296 and Codex 0.162.1 on October 11, 2026. This API extension remains a staging preview. Claude Desktop and public directory approval are separate distribution paths.
