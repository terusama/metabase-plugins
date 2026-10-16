# Connect Velostics

Choose test or staging before reading or changing records. Sign in to each connection separately.

| Environment | MCP connection | Codex sign-in |
| --- | --- | --- |
| Test | `velostics-test` | `codex mcp login velostics-test` |
| Staging | `velostics-staging` | `codex mcp login velostics-staging` |

In Claude Code, open `/mcp` and select the connection for the intended environment.

Use your Velostics account in Claude Code or Codex to find records, query data, and make the changes you can make on the website.

Preview: this package uses nonproduction data and requires an invited preview account. Use it only with nonproduction records.

## Connect and ask

1. Ask your assistant: **"Connect Velostics."** It will check the connection and guide you to sign in if needed.
2. Sign in with your Velostics account in the browser, then return to your conversation. An existing sign-in session can take you straight back.
3. Ask: **"Show my Velostics profile"**, **"Find my upcoming appointments"**, or **"Show five recent analytics records."** To make a change, describe what you want changed.

Sign-in happens on `login.velostics.com`; keep passwords out of the conversation. Your account needs website access for website operations and analytics access for Metabase queries. A permission denial means the account cannot perform that request.

## Install once

Add the public marketplace, then install the plugin:

| Client | Add the marketplace | Install the plugin |
| --- | --- | --- |
| Claude Code | `claude plugin marketplace add terusama/velostics-plugins` | `claude plugin install velostics@velostics` |
| Codex | `codex plugin marketplace add https://github.com/terusama/velostics-plugins.git` | `codex plugin add velostics@velostics` |

Alternatively, download and extract the marketplace ZIP from the repository's releases. Open a terminal in its extracted folder and replace the marketplace address above with `.`.

Start a new conversation after installation, then follow **Connect and ask** above. No API key, local server, or velOS installation is required.

## Replace an earlier preview

If you installed `velostics-metabase`, replace it with the Velostics plugin:

1. Remove the earlier plugin and its marketplace using the commands for your client:

   | Client | Remove the earlier plugin | Remove the earlier marketplace |
   | --- | --- | --- |
   | Claude Code | `claude plugin uninstall velostics-metabase@velostics-metabase` | `claude plugin marketplace remove velostics-metabase` |
   | Codex | `codex plugin remove velostics-metabase@velostics-metabase` | `codex plugin marketplace remove velostics-metabase` |

2. Run the **Install once** commands above, then start a new conversation.
3. Ask **"Connect Velostics"** and sign in once for the renamed connection. Your account permissions stay the same.

Earlier preview packages keep their existing connections until you replace them.

## Open sign-in yourself

| Client | Start sign-in |
| --- | --- |
| Claude Code | Open `/mcp`, select the selected **velostics-test** or **velostics-staging** connection, and choose its sign-in action. |
| Codex | Run `codex mcp login <connection>` in your terminal. |

The browser page names the client you should return to. Never paste a password, access token, or Metabase API key into the conversation.

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

To remove the plugin, run `claude plugin uninstall velostics@velostics` or `codex plugin remove velostics@velostics` in your terminal.

## Data handling

Your client sends requests to the hosted gateway, which verifies your sign-in. Website calls go to Velostics with your user identity; Metabase queries resolve your organization's analytics access. Results enter your agent conversation, where your Claude or Codex provider's data policies also apply. This archive contains public connection settings and instructions; it contains no user credentials or tenant data.

## Compatibility and release status

This preview uses the test and staging websites and nonproduction analytics data. Claude Code and Codex are supported. Claude Desktop and public directory approval are separate distribution paths.
