---
layout: default
title: Settings
---

# Settings

Click the gear icon at the top of the chat window. Settings are saved to
`%LOCALAPPDATA%\SsmsChatExtension\settings.json` when you click **Save**.

![Settings]({{ '/assets/img/settings-claude.png' | relative_url }})

| Setting | Meaning |
| --- | --- |
| Repository folder | Where Claude works and may edit files. Empty = a private scratch folder (`...\SsmsChatExtension\workspace`). |
| Claude permissions | See [below](#claude-permissions). |
| Let Claude run SQL that changes the database | See [below](#database-changes). |
| Model | `--model`: `opus`, `sonnet`, `haiku`, `fable` or any model id. Empty = Claude Code's default. |
| Effort | `--effort`: `low`, `medium`, `high`, `xhigh`, `max`. Empty = the model's default. |
| Connection string override | Optional. Used for database tools instead of the active query window's connection (stored DPAPI-encrypted for your Windows user). |
| Claude Code CLI path | Optional full path to `claude.exe` / `claude.cmd`. |

Theme and accent colour are not in this panel; they have their own [palette button](../themes/) and save
immediately.

## Claude permissions

For files and shell commands:

| Option | Claude Code mode | Effect |
| --- | --- | --- |
| Edit files in the repository folder *(recommended)* | `acceptEdits` | Claude can create and edit files in the repository folder |
| Auto mode | `auto` | Claude Code's safety classifier approves actions, including shell commands, and blocks risky ones |
| Read-only | `default` | Anything that needs permission is refused |

## Database changes

Applies in every Claude permission mode:

| Option | Effect |
| --- | --- |
| Off | `execute_sql` and `execute_query_window` refuse; Claude can still explore with `run_query` and put scripts in the editor |
| Ask me before each change *(default)* | SSMS shows the SQL, server / database and Claude's reason; nothing runs unless you click **Yes** |
| Allow without asking | Runs immediately. Only use this against development databases |

> The approval dialog is the safety net, so read it. For a hard guarantee, connect with a login that has only the
> permissions you want Claude to have.

## Project conventions

Add a `CLAUDE.md` to the repository folder to give Claude project conventions (naming, style, which databases
are which); the CLI picks it up automatically.
