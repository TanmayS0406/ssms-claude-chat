---
layout: default
title: FAQ
---

# FAQ and troubleshooting

## "Claude Code CLI not found"

Install Claude Code from [claude.com/claude-code](https://claude.com/claude-code), then click the refresh icon
next to the sign-in status. If it is installed somewhere unusual, set **Settings > Claude Code CLI path** to the
full path of `claude.exe` or `claude.cmd`.

## I don't see the window in SSMS

Open it from **View > SSMS Claude Chat**. If the menu item is missing, close SSMS and run the setup again. If SSMS
lives in a non-standard folder, pass `/SSMSPATH="...\Common7\IDE"` to the setup.

## Database tools say there is no connection

The tools use the **active query window**. Click into a query window that is connected, then ask again. For
Microsoft Entra logins that cannot be reused from SSMS, set a **connection string override** in Settings.

## Can Claude change my database without asking?

Only if you choose **Allow without asking** in Settings. The default asks before every change and shows the SQL.
`run_query` is read-only by design: statements that write, `EXEC`, transactions, `USE`, `OPENROWSET` and similar
are rejected, and every query also runs inside a transaction that is always rolled back.

## What is sent to Claude?

Your messages, the query context (if the chip is on), attachments, and whatever the tools return when Claude
calls them: object definitions, query results, file contents in the repository folder. It goes through the Claude
Code CLI under your own Claude account. See [Anthropic's privacy policy](https://www.anthropic.com/legal/privacy).

## What is stored on my machine?

Everything is under `%LOCALAPPDATA%\SsmsChatExtension`:

| Folder / file | Contents |
| --- | --- |
| `settings.json` | Settings, theme and accent (connection string override DPAPI-encrypted) |
| `history\` | One JSON file per chat |
| `attachments\` | Copies of attached files, kept 30 days |
| `diagrams\` | Generated diagram pages |

## The diagram page is blank

Rendering loads Mermaid from cdn.jsdelivr.net, so it needs internet access. The diagram source is always on the
page.

## Something else?

[Open an issue]({{ site.issues_url }}). Please include your SSMS version, the extension version and what you
expected to happen.
