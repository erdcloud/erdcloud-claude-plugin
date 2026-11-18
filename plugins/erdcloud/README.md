# ERDCloud for Claude Code

Connect Claude Code to [ERDCloud](https://www.erdcloud.com), the web-based diagramming service for database design. With this plugin Claude can read and edit your ERDCloud diagrams: ERD tables, columns, relations, domains and memos, and also sequence diagrams, flowcharts, UML class diagrams and free-form shapes on the same canvas. Edits appear live for everyone who has the diagram open.

## What is included

| Component | Purpose |
|---|---|
| MCP server `erdcloud` | Remote server at `https://www.erdcloud.com/mcp` that exposes the diagram tools. |
| Skill `erd-modeling` | Domain-first and relationship-first workflow for ERDs, plus an overview of the tools. |
| Skill `canvas-diagrams` | Which tool to use for sequence diagrams, flowcharts, UML class diagrams and shapes, and how to edit them. |
| Skill `erd-from-sql` | `/erdcloud:erd-from-sql <diagram URL> [file or description]` builds a diagram from SQL DDL or a description. |
| Skill `diagram-from-description` | `/erdcloud:diagram-from-description <diagram URL> <sequence\|flowchart\|class> <description or path>` draws a diagram from a description or from source code. |

## Install

In Claude Code 2.1.275 or later, add the marketplace and install in one command:

```
/plugin install erdcloud --marketplace erdcloud/erdcloud-claude-plugin
```

Or in two steps:

```
/plugin marketplace add erdcloud/erdcloud-claude-plugin
/plugin install erdcloud@erdcloud
```

Then restart Claude Code, run `/mcp`, select `erdcloud` and sign in to ERDCloud in the browser window that opens. Review the permission screen and click **Allow**. No token has to be copied.

## What the plugin does and what it sends

- The plugin contains only an MCP server declaration and skill instructions. It has no hooks, scripts, background processes or bundled binaries, and it does not run any local code.
- When you ask Claude to work on a diagram, Claude calls the ERDCloud MCP server over HTTPS. Table, column and shape names and the other diagram content that Claude reads or writes are sent to ERDCloud, and the text of your conversation that Claude includes in a tool call goes with it. Do not use it with schemas that must stay confidential.
- Sign-in uses OAuth. Claude can only reach diagrams that your ERDCloud account can access. Access tokens last one hour and are renewed automatically, and you can disconnect the app at any time in ERDCloud under **AI (MCP)** > **Connected apps**.
- Edits are applied live and can be wrong. Create a Snapshot or export a backup in ERDCloud before large changes.

## Links

- Service: <https://www.erdcloud.com>
- [Terms of Service](https://www.erdcloud.com/static/html/terms.html) and [Privacy Policy](https://www.erdcloud.com/static/html/privacy.html)
- License: [MIT](LICENSE)
