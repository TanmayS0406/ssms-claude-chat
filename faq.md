---
layout: default
title: SSMS Claude Chat FAQ and help
description: Answers to common questions about SSMS Claude Chat, the Claude AI add-in for SQL Server Management Studio. Cost, supported SSMS versions, privacy, safety and fixes for common problems.
---

# SSMS Claude Chat: questions and answers

## About SSMS Claude Chat

### What is SSMS Claude Chat?

A free add-in (extension) for SQL Server Management Studio that adds a Claude AI chat window. You can ask about
your database in plain English, get SQL explained or written, fix slow queries and draw diagrams.

### Is it free?

Yes, SSMS Claude Chat is free. You do need your own Claude plan (Pro, Max, Team or Enterprise) or a Claude
Console account, because the answers come from Claude.

### Which versions of SSMS does it work with?

SSMS 21 and SSMS 22 on Windows. Older versions (SSMS 20, 19, 18) aren't supported.

### Does it work with Azure SQL?

Yes. It uses the same connection as your query window, so it works with anything SSMS can connect to, including
SQL Server, Azure SQL Database and Azure SQL Managed Instance.

### Where do I download it?

From the [SSMS Claude Chat download page]({{ site.download_url }}). It always has the newest version. See
[How to install](../getting-started/).

## Safety and privacy

### Can Claude change my database without asking?

No, not unless you turn on **Allow without asking** in Settings. By default, every change shows you the exact SQL
and waits for you to click **Yes**. When Claude only looks at data, it can't change anything.

### What does Claude see?

Only what it needs to answer you: your messages, the text you've selected in the query window, files you attach,
and the table definitions or query results it looks up. It goes to Claude under your own account. See
[Anthropic's privacy policy](https://www.anthropic.com/legal/privacy).

### Is my Claude password stored?

No. You sign in to Claude in your browser. SSMS Claude Chat never sees your password.

### What is saved on my computer?

Your settings, chat history, attachment copies (kept 30 days) and diagrams, all in your Windows profile under
`%LOCALAPPDATA%\SsmsChatExtension`. Delete that folder to remove everything.

## Problems

### I can't find the chat window in SSMS

Click **View > SSMS Claude Chat**. If it isn't in the menu, close SSMS and run the setup again.

### It says "Claude Code CLI not found"

Install [Claude Code](https://claude.com/claude-code), then click the refresh button next to the sign-in status.
If you installed it in an unusual place, set its location in **Settings**.

### It says there is no connection

Click into a query window that's connected to a database, then ask again.

### Windows warns me when I run the setup

Click **More info**, then **Run anyway**. This can happen with any newly released download.

### The diagram page is blank

Diagrams need an internet connection to draw. The diagram text is still shown on the page.

### Something else?

[Report a problem]({{ site.issues_url }}) and tell us your SSMS version and what happened.
