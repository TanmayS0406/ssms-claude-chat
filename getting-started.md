---
layout: default
title: Getting started
---

# Getting started

Install the extension, sign in with Claude and ask your first question. It takes about five minutes.

## Requirements

- **SQL Server Management Studio 21 or 22** on Windows (x64 or Arm64).
- **Claude Code CLI** (`claude`) on the same machine. Install it from
  [claude.com/claude-code](https://claude.com/claude-code): the native installer (`~/.local/bin/claude.exe`)
  or `npm i -g @anthropic-ai/claude-code`. The chat window finds it on `PATH` or in those folders; otherwise set
  its path in **Settings**.
- A **Claude subscription** (Pro, Max, Team or Enterprise) or a Claude Console account to sign in with.

## Install

1. [Download the setup]({{ site.download_url }}) (version {{ site.latest_version }}).
2. Close SSMS and run the setup. It needs no admin rights.
3. Start SSMS and open **View > SSMS Claude Chat**.

Setup finds SSMS 21 / 22 and installs the extension with the `VSIXInstaller.exe` that ships with SSMS
(double-clicking a `.vsix` does not work for SSMS 21+). Running a newer setup upgrades in place.

| Setup option | Use it when |
| --- | --- |
| `/SSMSPATH="D:\...\Release\Common7\IDE"` | SSMS is installed in a non-standard folder |
| `/VERYSILENT` | Unattended install |

> If Windows shows a SmartScreen warning, click **More info > Run anyway**.

To uninstall: **Settings > Apps > Installed apps > SSMS Claude Chat**.

## Sign in

Click **Sign in** at the top of the chat window. It runs the official Claude Code sign-in
(`claude auth login`) in a console window and your browser. The extension never sees or stores your Claude
credentials; the CLI keeps them. The sign-out button runs `claude auth logout`.

## Your first chat

1. Open a query window connected to the database you want to talk about.
2. Type a question and press <kbd>Enter</kbd> (<kbd>Shift</kbd>+<kbd>Enter</kbd> adds a new line). For example:
   - *What does dbo.usp_GetOrders do, and why is it slow for big customers?*
   - *Draw an ER diagram of the Sales schema.*
   - *Write a procedure that archives orders older than two years.*
3. Leave the **Query context** chip on to send the selected text (or the whole query) of the active query
   window along with your message.

![Chat window]({{ '/assets/img/chat-light.png' | relative_url }})

## The toolbar

| Icon | What it does |
| --- | --- |
| ✎ New chat | Starts a new conversation; the current one stays in History |
| ⟲ History | Lists saved chats; open one to continue it, or delete it |
| ⛁ DB diagram | ER diagram of the active connection's databases, drawn from the catalog (no AI call) |
| 🎨 Theme | Theme and accent colour, see [Themes](../themes/) |
| ⚙ Settings | Repository folder, permissions, model and effort, see [Settings](../settings/) |

Next: [everything Claude can do](../features/).
