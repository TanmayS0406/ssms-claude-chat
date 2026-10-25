---
layout: default
title: Features
---

# Features

Claude is instructed to stay on topic: SQL Server, T-SQL, stored procedures, schema design, performance, SSMS and
the scripts in your repository. Other requests get a one-line polite refusal.

## Understands your database

Claude gets tools for the server and database of the **active query window**:

| Tool | What it does |
| --- | --- |
| `get_connection_info` | Server, database and login of the active window |
| `list_databases`, `list_objects` | What is there |
| `describe_object` | Columns, keys, indexes, foreign keys, parameters, row count and the full definition |
| `get_dependencies` | What an object uses and what uses it |
| `run_query` | Read-only queries (always rolled back, 30 s timeout, row limit) |

## Stored procedures

Claude reads a procedure's definition and dependencies before explaining it, writes new or changed procedures as
`CREATE OR ALTER` in the editor or your repository, deploys them with `execute_sql` when you ask, and runs them
with `EXEC`, subject to the [database change setting](../settings/#database-changes).

## Diagrams

- Ask for a flowchart of a procedure, an ER diagram of some tables or a call chain, and Claude opens a Mermaid
  diagram in your browser with *Download SVG* and *Copy source* buttons.
- The **DB diagram** button draws an ER diagram straight from the catalog, with no AI call and no tokens used.
  Tick one or more databases (and optionally a schema):
  - **Solid lines** are declared foreign keys.
  - **Dashed lines** are *inferred* relationships, e.g. `Invoices.CustomerId` → `Customers.Id`, including links
    **across databases**, which SQL Server cannot declare. Review them; they are guesses.
  - Each database gets its own colour. Large selections are trimmed to 200 tables.

## Runs SQL for you, with your approval

`execute_sql` runs any script (`INSERT` / `UPDATE` / `DELETE`, `CREATE` / `ALTER`, `EXEC`, `GO` batches) and
`execute_query_window` presses F5 on the active query window so you see the results grid. By default SSMS shows
the SQL, the server / database and Claude's reason first, and nothing runs unless you click **Yes**.

After objects are created, altered or dropped, Object Explorer and IntelliSense refresh automatically.

## Edits query windows and your repository

- `get_query_window`, `replace_query_window` (one <kbd>Ctrl</kbd>+<kbd>Z</kbd> undoes it) and
  `open_new_query_window` (connected like the active window).
- Claude works in the *repository folder* from Settings and can create and edit files there. Read-only
  `git status / diff / log / show` are always allowed.

## Attachments

**Attach** (paper clip) picks files: SQL scripts, `.sqlplan` execution plans, logs, CSV, images, PDF (up to 10
per message, 20 MB each). You can also drop files on the message box. **Screenshot** opens the Windows snipping
overlay; <kbd>Ctrl</kbd>+<kbd>V</kbd> in the message box attaches a copied image or copied files.

## Chat history

Every conversation is saved to `%LOCALAPPDATA%\SsmsChatExtension\history`. Opening one from **History** continues
the same Claude session, so Claude still remembers it.

![History]({{ '/assets/img/history-nord.png' | relative_url }})

## Model and effort

Pick the model (`opus`, `sonnet`, `haiku`, `fable`, or type any model id) and the effort level (`low` … `max`) in
Settings; the header shows what is active.

## How it works

```
SSMS Claude Chat window ──stdin──▶ claude -p --output-format stream-json --resume <session>   (cwd = repository folder)
       ▲                         │  built-in tools: Read / Edit / Write / Grep ... inside the repository
       └──── streamed reply ─────┤
                                 └─ MCP over http://127.0.0.1:<random port>/mcp  (random bearer token)
                                        └─ "ssms" tools inside SSMS: database + query windows
```

Database tools use the connection of the active query window, created by SSMS itself, so Windows, SQL and
Microsoft Entra logins all work.
